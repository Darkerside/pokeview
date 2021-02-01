<template>
  <div class="pokemon__navigation">
    <div class="prev"><button :disabled="pokeList[0] === null" @click="loadPrevList">Prev</button></div>
    <div class="index">{{ indexNavInfo }}</div>
    <div class="next"><button :disabled="pokeList[1] === null" @click="loadNextList">Next</button></div>
  </div>
</template>

<script>
export default {
  name: 'PokemonNavigation',
  props: {
    pokeList: Array,
    pokemonListIndex: Number,
    pokemonMaxIndex: Number
  },
  data() {
    return {
      indexNavInfo: ''
    }
  },
  methods: {
    loadNextList() {
      this.$emit('load-next')
    },
    loadPrevList() {
      this.$emit('load-prev')
    },
    showindex() {
      this.indexNavInfo = `${this.pokemonListIndex} of ${this.pokemonMaxIndex}`
    }
  },
  mounted() {
    this.showindex()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.pokemon__navigation {
  padding: 15px 1em;
  display: flex;
  flex-flow: row;
  justify-content: space-between;
  max-width: 1300px;
  margin: 0 auto;
}

.pokemon__navigation button {
  background-color: #42b983;
  box-shadow: 0 2px 5px 0 rgba(0,0,0,0.16), 0 2px 10px 0 rgba(0,0,0,0.12);
  border: 2px solid #42b983;
  border-radius: 5px;
  color: white;
  padding: 8px 16px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  transition-duration: 0.4s;
  cursor: pointer;
}

.pokemon__navigation button:hover {
  background-color: white;
  color: #42b983;
  border: 2px solid #42b983;
}

.pokemon__navigation button:disabled {
  background-color: #befde1;
  border: 2px solid #befde1;
  border-radius: 5px;
  color: rgb(184, 184, 184);
  box-shadow: 0 0 0 0 rgba(0,0,0,0.16), 0 0 0 0 rgba(0,0,0,0.12);
  padding: 8px 16px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: default;
}

.index {
  margin: auto;
  color: #a0a0a0;
}

</style>
