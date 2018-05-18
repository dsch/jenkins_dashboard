<template>
  <div id="app">
    <JobsStatus v-bind:jobs="jobs"/>
  </div>
</template>

<script>
import JobsStatus from './components/JobsStatus'

function extractJson (response) {
  return response.json()
}

function getStatus (data) {
  return data.building ? 'building' : (data.result === 'SUCCESS') ? 'success' : 'failure'
}

function buildJobData (name, data) {
  return {
    name: name,
    status: getStatus(data),
    timestamp: new Date(data.timestamp)
  }
}

export default {
  name: 'App',
  components: {
    JobsStatus
  },
  data () {
    return {
      url: '/static/jenkins/view/api.json',
      jobs: [ ]
    }
  },
  created: function () {
    var vm = this
    fetch(vm.url)
      .then(extractJson)
      .then(function (data) {
        Promise.all(data.jobs.map(function (job) {
          return fetch(job.url)
            .then(extractJson)
            .then(function (data) {
              return buildJobData(job.name, data)
            })
        })).then(function (jobs) {
          vm.jobs = jobs
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
