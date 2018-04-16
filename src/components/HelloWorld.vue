<template>
  <ul class="hello">
    <li v-for="job in jobs" :key="job.id">{{ job.name }}</li>
  </ul>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      jobs: [
        {id: 1, name: 'Welcome to Your Vue.js App'},
        {id: 2, name: 'Welcome 2'}
      ]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
