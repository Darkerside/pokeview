<template>
  <div class="pokemon__card-info">
    <img :src="'https://pokeres.bastionbot.org/images/pokemon/' + pokemonId + '.png'" class="pokemon-icon">
    <p class="pokemon-name">{{ pokemonName }}</p>
  </div>
</template>

<script>
export default {
  name: 'PokemonCard',
  props: {
    pokemonInfo: JSON
  },
  data() {
    return {
      pokemonImgBase: 'https://pokeres.bastionbot.org/images/pokemon/',
      pokemonId: null,
      pokemonName: ''
    }
  },
  methods: {
    getPokemonId() {
      let splittedStr = this.pokemonInfo.url.split('/')
      this.pokemonId = splittedStr[splittedStr.length-2]
    },
    renamePokemon() {
      this.pokemonName = this.pokemonInfo.name.replace(/-/g,' ');
    }
  },
  mounted() {
    this.getPokemonId(),
    this.renamePokemon()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.pokemon__card-info {
    width: fit-content;
    margin: 0 auto;
    cursor: pointer;
    transition: all 0.25s ease;  
    text-align: center;
}

.pokemon__card-info:hover {
  transform: scale(1.1, 1.1);
}

.pokemon__card-info:hover .pokemon-icon {
  box-shadow: 0 2px 5px 0 rgba(102, 240, 178, 0.5), 0 2px 10px 0 rgba(102, 240, 178, 0.5);
}

.pokemon__card-info:hover .pokemon-name {
  color: #42b983
}

.pokemon-icon {
  max-width: 75px;
  padding: 5px;
  border: 1px solid rgba(0,0,0,0.16);
  border-radius: 0.25em;
  box-shadow: 0 2px 5px 0 rgba(0,0,0,0.16), 0 2px 10px 0 rgba(0,0,0,0.12);
}

.pokemon-name {
  margin: 10px auto;
  font-weight: 500;
}

@media (min-width: 601px) and (max-width: 864px) {
  .pokemon-icon {
    max-width: 95px;
  }
}

@media (min-width: 865px) {
  .pokemon-icon {
    max-width: 120px;
  }
}

</style>
