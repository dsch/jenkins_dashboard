<template>
  <div id="app">
    <JobsStatus v-bind:jobs="jobs"/>
  </div>
</template>

<script>
import JobsStatus from './components/JobsStatus'

export default {
  name: 'App',
  components: {
    JobsStatus
  },
  data () {
    return {
      jobs: [
        {id: 1, name: 'E16019 Application', timestamp: new Date(1520022023650), status: 'failure'},
        {id: 2, name: 'E16019 Bootloader', timestamp: new Date(1520022023650), status: 'success'},
        {id: 3, name: 'E16016 Bootloader', timestamp: new Date(1520022023650), status: 'building'}
      ]
    }
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
