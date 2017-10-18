<template>

<div>
    <h2>{{msg}}}</h2>
    <div class="content">
      <video id="publisher-video"></video>
    </div>
    <div class="control">
      <button @click="joinRoom()">Join Room</button>
      <button @click="mute()"> Mute / Unmute</button>
      <button @click="dropCall()">End Call</button>
    </div>
</div>

</template>


<script>
import config from '../config/tokbox.config'

export default {
  name: 'Room',
  props: ['id'],
  data () {
    return {
      msg: `Welcome Aboard`
    }
  },
  methods: {
    joinRoom: () => {
      console.log('Join Room', config.apiKey, this.id)
    },

    mute: () => {
      console.log('Mute Called')
    },

    dropCall: () => {
      console.log('Drop call')
    }
  }
}
</script>
<style scoped>
h1, h2 {
  font-weight: normal;
}

div.content{
  width: 80%;
  height: auto;
  margin: 0 auto;
}

div.control {
   margin: 12px auto;

}

video#publisher-video{
  width: 60%;
  box-shadow: 0px 2px 6px 0px;
}
</style>
