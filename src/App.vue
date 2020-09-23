<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <div>{{ recep }}</div>
  <button v-on:click="sendMessage(1)">Enviar inicio al servidor</button>
</template>

<script>
import SocketIO from 'socket.io-client'
 



export default {
  name: 'App',
  data() {
    return {
      connection: null,
      recep: "algun nombre"
    };
  },
  methods: {
    sendMessage: function(message) {
      // conect the socket
      this.connection = SocketIO('http://localhost:3000/');
      this.connection.emit('send_emit', message);
      this.connection.on('emit_message', function(msg){
        console.log("si esta adentro" + msg);
        this.recep = msg + " - ";
        console.log(this.recep);
      });
    },
  },
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
