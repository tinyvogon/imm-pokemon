 <template>
  <div>
    <div class="card" style="width: 18rem;">
        <img v-bind:src="pokemon.sprites.front_default" class="card-img-top" alt="...">
    <div class="card-body">
        <h5 class="card-title">{{ pokemon.name }}</h5>
        <p class="card-text"> 
            <p>Height: {{pokemon.weight}} lbs</p>
            <p>Weight: {{pokemon.height}} inches</p>
          
        </p>
        <a href="#" class="btn btn-primary">Go somewhere</a>
    </div>
</div>
  </div>
</template>

<script>
    export default {
    name: 'card',
    data: function() {
        return {
        pokemon: null
        }
    },
    props: {
        msg: String
    },
    mounted: function(){
        console.log("mounted function ran");
        const axios = require('axios');
        const vm = this;
        axios({
        method: 'get',
        url: 'https://pokeapi.co/api/v2/pokemon/chikorita',
        responseType: 'stream'
        })
        .then(function (response) {
            console.log(response.data);
            vm.pokemon = response.data

        });
    }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped> 
h3 {
  margin: 40px 0 0;
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
