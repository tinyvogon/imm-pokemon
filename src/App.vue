<template>
  <div id="app">
    <div class="container">  
      <h2 class="text-center display-1 m-5 text-capitalize"> {{ activeType }} Type Pokemon </h2>
      <span v-for="item in types" class="btn btn-primary m-1" v-on:click="somethingHappened(item.name)" :key="item">
        {{item.name}}
      </span>
      <br><br>
      <div class="row">
        <card :url="item.pokemon.url" v-for="item in pokemonOfCurrentType" :key="item.pokemon.name"></card>
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
        pokemonOfCurrentType: "",
        types: "",
        activeType: "rock"
        }
  },
  methods:{
    somethingHappened: function(name){
      this.activeType = name;
      this.retrievePokemonOfSpecifiedType(this.activeType)
    },
    retrievePokemonOfSpecifiedType: function(type){
      const axios = require('axios');
      const vm = this;
      axios({
        method: 'get',
        url: 'https://pokeapi.co/api/v2/type/' + type
        })
      .then(function (response) {
        //console.log(response.data.pokemon);
        vm.pokemonOfCurrentType = response.data.pokemon
        });
    }
  },
  mounted: function(){
      const axios = require('axios');
      const vm = this;
      console.log("mounted function ran");
      this.retrievePokemonOfSpecifiedType(this.activeType)
      axios({
        method: 'get',
        url: 'https://pokeapi.co/api/v2/type'
        })
      .then(function (response) {
        //console.log(response.data);
        vm.types = response.data.results
        });
  }  
}
</script>

<style>

</style>
