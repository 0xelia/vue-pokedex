<template>
  <div id="app" class="h-screen flex flex-col">
    <SearchBar :text="title" @onPokeRes="getRes" />

    <ShowRes v-if="status === 200" 
    :pokemon="pokemon" :pics="pokePics"
    @onPokeClick="getPokedex"  />

    <pokedexPreview :pokedex="pokedex" 
    @onPokeRemove="removeFromPokedex" @onPokeShow="getPokeToShow" />
  </div>
</template>

<script>
import SearchBar from './components/SearchBar.vue';
import ShowRes from './components/ShowRes.vue';
import pokedexPreview from './components/pokedexPreview.vue';

export default {
  name: 'App',
  data(){
    return{
      title: 'Cerca un Pokemon',
      pokemon: {},
      pokePics: {},
      pokedex: [],
      status: null,
    }
  },

  components: {
    SearchBar,
    ShowRes,
    pokedexPreview
  },

  methods: {
    getRes(pokeData){
      const {data} = pokeData
      const {status} = pokeData

      this.pokemon = data
      this.status = status

      const {sprites} = this.pokemon
      this.pokePics = sprites
  
    },

    getPokeToShow(data){
      return this.pokemon = data
    },

    removeFromPokedex(data){
      const poke = data

      this.pokedex = this.pokedex.filter(el => el.id != poke.id)
      return this.pokedex
  
    },

    getPokedex(data){
      this.pokedex = data

      console.log(this.pokedex)
    },
  },

}
</script>

<style lang="scss">
  #app{
    height: 100vh;
  }
</style>
