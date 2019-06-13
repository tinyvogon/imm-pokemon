<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Hewwo thewe"/>
    <card :url="item.pokemon.url" v-for="item in pokemonOfRockType" :key="item"></card>
    
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import card from './components/card.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    card
  },
  data: function() {
    return {
        pokemonOfRockType: ""
        }
  },
  mounted: function(){
      console.log("mounted function ran");
      const axios = require('axios');
      const vm = this;
      axios({
        method: 'get',
        url: 'https://pokeapi.co/api/v2/type/rock',
        responseType: 'stream'
        })
      .then(function (response) {
        //console.log(response.data.pokemon);
        vm.pokemonOfRockType = response.data.pokemon
        });
  }  
}
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
