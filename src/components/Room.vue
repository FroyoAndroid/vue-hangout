<template>
  <div>
    <h2>{{msg}}</h2>
    <div class="content">
      <video id="publisher-video"></video>
    </div>
    <div class="control">
      <button @click="joinRoom(sessionID)">Join Room</button>
      <button @click="mute()"> Mute / Unmute</button>
      <button @click="dropCall()">End Call</button>
    </div>
  </div>
</template>


<script>
import config from '../config/tokbox.config'
import axios from 'axios'

let session = null
// let publisher = null
export default {
  name: 'Room',
  props: ['id'],
  data () {
    return {
      msg: `Welcome Aboard`,
      sessionID: this.$route.params.id
    }
  },
  methods: {
    joinRoom (sessionId) {
      session = window.OT.initSession(config.apiKey, sessionId)
      setTimeout(() => {
        this.bindSessionEvents(session)
      }, 300)
      axios.post('http://localhost:3000/rooms/token', {
        sessionID: sessionId,
        username: 'test'
      }).then((response) => {
        session.connect(response.data.token, (error) => {
          if (error) {
            console.error('Error', error)
          }
        })
      }).catch((error) => {
        console.error(error)
      })
    },

    bindSessionEvents (session) {
      console.log('session', session.connection.connectionId)
      session.off().on('connectionCreated', (event) => {
        if (event.connection.connectionId !== session.connection.connectionId) {
          console.log('Attending joining', event.connection.connectionId)
        } else {
          console.log('connection created', event.connection.connectionId)
        }
      })

      session.off().on('sessionDisconnected', (event) => {
        console.log('session disconnecting')
      })

      session.off().on('streamDestroyed', (event) => {
        console.log('stream disconnected')
      })
    },

    mute () {
      console.log('Mute Called')
    },

    dropCall () {
      session.disconnect()
      session = null
      console.log('Drop call')
    }
  }
}
</script>
<style scoped>
h1,
h2 {
  font-weight: normal;
}

div.content {
  width: 80%;
  height: auto;
  margin: 0 auto;
}

div.control {
  margin: 12px auto;
}

video#publisher-video {
  width: 60%;
  box-shadow: 0px 2px 6px 0px;
}
</style>
