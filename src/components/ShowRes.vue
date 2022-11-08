<template>
    <section class="container text-slate-500 grow">

        <h2 class="text-4xl">
            Ecco i risultati per <span class="font-bold"> {{ pokemon.name }} </span>
        </h2>

        <ul class="flex justify-around pt-12 pb-4 border border-t-0 border-x-0 border-slate-200">
            <li>
                Nome: {{ pokemon.name }}
            </li>
            <li>
                Altezza: {{ pokemon.height }}
            </li>
            <li>
                Peso: {{ pokemon.weight }}
            </li>
        </ul>


        <!-- Pokemon card -->
        <div class="h-[475px] grid grid-cols-2">

            <!-- poke pic and buttons -->
            <div class="flex flex-col ">
                <div class="pic flex grow">

                    <figure class="h-full flex justify-center items-center grow">

                        <img :src="shiny ? pokemon.sprites.front_shiny : pokemon.sprites.front_default" class="h-60 " alt="">
    
                    </figure>

                    <div class="flex flex-col self-center mr-4 gap-4">
    
                        <button @click="shiny = false" class="px-8 py-4 text-purple-700 border border-purple-700 rounded">
                            Defult
                        </button>
                        <button  @click="shiny = true" class="px-8 py-4 bg-purple-700 text-white rounded">
                            Shiny
                        </button>
    
                    </div>
                    
                </div>

                    <button v-if="!pokedex.includes(pokemon)" @click="$emit('onPokeClick', {pokemon, add: true}), setBadge()"
                    class="px-8 py-2 mb-6 bg-purple-700 rounded text-white w-1/2 self-center">
                        Aggiungi al Pokedex
                    </button>
                    <button v-if="pokedex.includes(pokemon)" @click="$emit('onPokeClick', {pokemon, remove: true})" 
                    class="px-8 py-2 mb-6 bg-purple-700 rounded text-white w-1/2 self-center">
                        Rimuovi dal Pokedex
                    </button>
            </div>

            <!-- poke stats -->
            <ul class="flex flex-col justify-center gap-6">

                <h3 class="text-2xl">
                    Statistiche
                </h3>

                <li v-for="(stat, i) in pokemon.stats" :key="i">
                    <p class="mb-2">
                        {{ stat.stat.name }}
                    </p>
                    <div class="h-2 w-4/6 relative rounded-full bg-slate-200 overflow-hidden">
                        <div :style='`width:${stat.base_stat}%`' class="absolute top-0 bottom-0 bg-purple-700 "></div>
                    </div>
                </li>

            </ul>

        </div>

        <div v-if="showBadge" class="badge px-16 py-8 font-bold bg-slate-300/50 text-white text-xl fixed left-2/4 bottom-2/4 backdrop-blur-lg rounded-md">
            <p>
                Il tuo pokedex è pieno!
            </p>
        </div>


    </section>
</template>

<script>


    export default {

        props:{
            pokemon: Object,
            pokedex: Array
        },

        data(){
            return{
                showBadge: false,
                shiny: false
            }
        },

        methods: {
            setBadge(){
                if(this.pokedex.length == 10){
                    this.showBadge = true
                }

                if(this.showBadge){
                    setTimeout(() => {
                        this.showBadge = false
                    },2000)
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
    .badge{
        transform: translateX(-50%);
        transition: all 700ms linear;
    }
</style>