<template>
  <ul class="jobs">
    <li v-for="job in jobs" :key="job.id" v-bind:class="job.status">
      <div class="name">{{ job.name }}</div>
      <div class="status">{{ job.status }}</div>
      <div class="timestamp">{{ job.timestamp }}</div>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'JobsStatus',
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
}

.timestamp {
  opacity: 0.5;
}

li.failure {
  background-color: #8b0000;
}

li.success {
  background-color: #006400;
}

li.building {
  background-color: #00008d;
}
</style>
