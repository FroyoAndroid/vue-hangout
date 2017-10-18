<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <ul>
      <li v-for="room in rooms"><a v-bind:href="'#/'+room.sessionID" target="_blank">{{room.room}}</a></li>
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
    axios.get(`http://localhost:3000/rooms`)
    .then(response => {
      // JSON responses are automatically parsed.
      console.log(response.data)
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
