<template>
  <div id="app">
    <JobsStatus v-bind:jobs="jobs"/>
  </div>
</template>

<script>
import JobsStatus from './components/JobsStatus'
import IntlRelativeFormat from 'intl-relativeformat'

const rf = new IntlRelativeFormat('en-US')

function getStatus (data) {
  return data.building ? 'building' : (data.result === 'SUCCESS') ? 'success' : 'failure'
}

function buildJobData (name, data) {
  const date = new Date(data.timestamp)
  return {
    name: name,
    status: getStatus(data),
    date: date,
    timestamp: rf.format(date)
  }
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
        Promise.all(data.jobs.map(function (job) {
          return fetchJenkinsJsonApi(job.url + '/lastBuild')
            .then(function (data) {
              return buildJobData(job.name, data)
            })
        })).then(function (jobs) {
          vm.jobs = jobs.sort(function (a, b) {
            return b.date - a.date
          })
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
