<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <ul>
      <li v-for="room in rooms"><a href="https://vuejs.org" target="_blank">{{room}}</a></li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Choose rooms to join',
      rooms: []
    }
  },
  created () {
    axios.get(`http://stream.eu-4.evennode.com/rooms`)
    .then(response => {
      // JSON responses are automatically parsed.
      console.log(response.status)
      this.rooms = response.data
    })
    .catch(e => {
      this.rooms.push(e)
    })
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
