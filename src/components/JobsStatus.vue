<template>
  <ul class="jobs">
    <li v-for="job in jobs" :key="job.url" v-bind:class="job.status">
      <div class="name">{{ job.name }}</div>
      <div class="status">{{ job.status }}</div>
      <div class="timestamp">{{ job.timestamp }}</div>
      <!--<div class="loader"></div>-->
    </li>
  </ul>
</template>

<script>
export default {
  name: 'JobsStatus',
  props: {
    jobs: Array
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}

li {
  border-radius: 5px;
  display: block;
  padding: 20px;
  margin: 10px;
  position: relative;
}

.timestamp {
  opacity: 0.5;
}

li.aborted, li.failure {
  background-color: #8b0000;
}

li.success {
  background-color: #006400;
}

li.building {
  background-color: #00008d;
}

li.loading {
  background-color: #8d8d8d;
}

.loader {
  border: 8px solid #f3f3f3; /* Light grey */
  border-top: 8px solid #3498db; /* Blue */
  border-radius: 50%;
  width: 40px;
  height: 40px;
  animation: spin 2s linear infinite;
  position: absolute;
  top: 10px;
  left: 10px;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>
