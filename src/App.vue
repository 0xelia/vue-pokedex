<template>
  <div id="app" class="h-screen flex flex-col">
    <SearchBar :text="title" @onPokeRes="getRes" />

    <ShowRes 
    :pokemon="pokemon" :pokedex="pokedex"
    @onPokeClick="getPokemon"  />

    <pokedexPreview :pokedex="pokedex" 
    @onPokeClick="getPokemon"  />
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
    },

    getPokemon(data){
      console.log(data)

      if(data.add){
        this.addPokemon(data.pokemon)
      } else if(data.remove){
        this.removePokemon(data.pokemon)
      } else if(data.show){
        this.pokemon = data.pokemon
      }

      console.log(this.pokedex)
    },

    addPokemon(pokemon){
      if(!this.pokedex.includes(pokemon)){
        this.pokedex.push(pokemon)
      }
    },  

    removePokemon(pokemon){
      this.pokedex = this.pokedex.filter(el => el.id != pokemon.id)
      return this.pokedex
    },

    getPokedex(data){
      this.pokedex = data
    },
  },

}
</script>

<style lang="scss">
  #app{
    height: 100vh;
  }
</style>
