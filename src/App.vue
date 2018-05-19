<template>
  <div id="app">
    <JobsStatus v-bind:jobs="jobs"/>
  </div>
</template>

<script>
import JobsStatus from './components/JobsStatus'
import IntlRelativeFormat from 'intl-relativeformat'

const rf = new IntlRelativeFormat()

function getStatus (data) {
  return data.building ? 'building' : (data.result === 'SUCCESS') ? 'success' : 'failure'
}

function updateJobStatus (job, build) {
  const date = new Date(build.timestamp)
  job.status = getStatus(build)
  job.date = date
  job.timestamp = rf.format(date)
}

function fetchJenkinsJsonApi (url) {
  return fetch(url + '/api/json')
    .then(function (response) {
      return response.json()
    })
}

export default {
  name: 'App',
  components: {
    JobsStatus
  },
  data () {
    return {
      // url: 'https://jenkins.mono-project.com/view/Components/api/json',
      url: '/static/jenkins/view',
      jobs: [ ]
    }
  },
  created: function () {
    const vm = this
    fetchJenkinsJsonApi(vm.url)
      .then(function (data) {
        vm.jobs = data.jobs.map(function (job) {
          const newJob = {
            name: job.name,
            url: job.url,
            status: 'loading'
          }
          fetchJenkinsJsonApi(newJob.url + '/lastBuild')
            .then(function (build) {
              updateJobStatus(newJob, build)
              vm.jobs = vm.jobs.sort(function (a, b) {
                return b.date - a.date
              })
            })
          return newJob
        })
      })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
  margin-top: 60px;
}

html {
  background-color: #000000;
}
</style>
