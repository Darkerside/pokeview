<template>
  <div id="app">
    <nav>
      <div class="navigation__logo">
        Pokeview - Making web in 2h
      </div>
    </nav>
    <div class="loader-container" v-if="pokemonData === null">
      <div class="loader"></div>
    </div>
    <PokemonList :pokemonData="pokemonData"/>
    <PokemonNavigation v-if="indexCount !== null" :pokeList="pokeList" :pokemonListIndex="listIndex" :pokemonMaxIndex="indexCount" @load-next="getNextList" @load-prev="getPrevList" :key="listIndex"/>
  </div>
</template>

<script>
import PokemonList from './components/PokemonList.vue'
import PokemonNavigation from './components/PokemonNavigation'

export default {
  name: 'App',
  components: {
    PokemonList, PokemonNavigation
  },
  data() {
    return {
      pokemonData: null,
      pokeList: [ null, null ],
      indexCount: null,
      listIndex: 24,
      baseApiEndPoint: 'https://pokeapi.co/api/v2/pokemon?limit=24&offset=0'
    }
  },
  methods: {
    getDataFromAPI(endPoint) {
      fetch(endPoint)
        .then( response => response.json())
        .then( data => {
            this.indexCount = data.count,
            this.pokeList = [data.previous, data.next]
            this.pokemonData = data.results
        })
    },
    getNextList(){
      this.getDataFromAPI(this.pokeList[1])
      this.listIndex = this.listIndex + 24;
    },
    getPrevList(){
      this.getDataFromAPI(this.pokeList[0])
      this.listIndex = this.listIndex - 24;
    }
  },
  mounted() {
    this.getDataFromAPI(this.baseApiEndPoint)
  }
}
</script>

<style>

body {
  margin: 0;
}

#app {
  font-family: Roboto, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #F3F5FA;
}

nav {
  position: sticky;
  z-index: 100;
  top: 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 5%;
  background-color: #42b983;
  color: white;
  box-shadow: 0 2px 5px 0 rgba(0,0,0,0.16), 0 2px 10px 0 rgba(0,0,0,0.12);
}

.navigation__logo {
  font-weight: bold;
  font-size: 24px;
}

.navigation__user {
  font-weight: bold;
}

.loader-container {
  margin-top: 3.5em;
}

.loader {
  border: 16px solid #f3f3f3; /* Light grey */
  border-top: 16px solid #42b983; /* Blue */
  border-radius: 50%;
  width: 120px;
  height: 120px;
  margin: 0 auto;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

</style>
