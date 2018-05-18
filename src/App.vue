<template>
  <div id="app">
    <JobsStatus/>
  </div>
</template>

<script>
import JobsStatus from './components/JobsStatus'

export default {
  name: 'App',
  components: {
    JobsStatus
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
