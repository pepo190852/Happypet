<template>
  <div id="app">
    <img src="./assets/logo.gif">
    <HelloWorld/>
    <p><img src="./assets/rc_c_stand.gif"></p>
    <p><button v-on:click="feeding(1)">Raccoon</button></p>
    <p><img src="./assets/slime.gif"></p>
    <p><button v-on:click="feeding(2)">Slime</button></p>
    <p><img src="./assets/egg.gif"></p>
    <p><button v-on:click="feeding(3)">Egg</button></p>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data: function() {
    return {
      connection: null
    }
  },
  created: function() {
    console.log("Starting connection to WebSocket Server")
    this.connection = new WebSocket("ws://172.20.10.3:3502/")

    this.connection.onmessage = function(event) {
      console.log(event);
    }

    this.connection.onopen = function(event) {
      console.log(event)
      console.log("Successfully connected to the echo websocket server...")
    }
    this.connection.onerror  = function(event){
      console.log(event)
    }

  },
  methods: {
    feeding: function(message) {
      //alert("Feeded"); //ยังไม่ได้ต่อ
      console.log(this.connection);
      var msg = {
        type:"action",
        message:'API.feeding', // message {API.feeding, API.playing,}
        player_id: 1,
        pet_id: message,
        skin_id : 8
    }
      this.connection.send(JSON.stringify(msg));
      alert("Feeded"); //ให้อาหารได้หลังจากต่อไปแล้ว
    }
  },
}
//import WebSocket from 'ws'
//const WebSocket = require('ws');
// export default {
//   name: 'App',
//   components: {
//     HelloWorld
//   }
// }
//   methods:{
//     feeding: function(msg){
      

// this.ws = new WebSocket('ws://10.80.10.118:3502/');

// this.ws.onopen = function(event){
//   alert("connect")
// }
// ws.on('open', function open() {
//   alert("connect")
//   /* authenticate first
//      get value from form ()   
//   */
//     var msg = {
//         type:"action",
//         message:'API.feeding', // message {API.feeding, API.playing,}
//         player_id: 1,
//         pet_id: msg,
//         skin_id : 8
//     }
//     ws.send(JSON.stringify(msg))
//     console.log('send');
// });
// ws.on('error',function error(error){
//     console.log(error)
// })

// ws.onmessage = function(event){
//     var json = JSON.parse( event.data);
//     //console.log('Message from server ', json["event"]);
//     Catalize(json)
//     //console.log(e)
// }

// const Catalize = (event) => {
//     console.log(String(event.event))
//     if(event.event === "list_all_skin"){
//         console.log(event["data"])
//     }
// }

// const blobToImage = (blob) => {
//     return new Promise(resolve => {
//       const url = URL.createObjectURL(blob)
//       let img = new Image()
//       img.onload = () => {
//         URL.revokeObjectURL(url)
//         resolve(img)
//       }
//       img.src = url
//     })
//   }
//     }
//   }
// }
//   }
// }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
