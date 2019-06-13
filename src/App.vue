<template>
  <div id="app">
    <div class="container">  
      <h1 class="text-center display-1 m-5"> Rock Type Pokemon </h1>
      <div class="row">
        <card :url="item.pokemon.url" v-for="item in pokemonOfRockType" :key="item"></card>
      </div>
    </div>
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

</style>
