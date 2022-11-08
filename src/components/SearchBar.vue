<template>
    <div :class="[pokedex.length == 0 ? 'grow' : '' ,'searchbar container py-6']">
        <h1 class="text-lg font-bold mb-4">
            {{text}}
        </h1>
        <div class="searchbar relative group flex flex-col">

            <div class="flex items-center">

                <input @keyup.enter="fetchPokemon(query), showLoader()" v-model="query" 
                class="border border-r-0 border-slate-300 rounded rounded-r-none w-full px-6 h-16" type="text"  placeholder="es. Pikachu" name="query" id="">
                <i @click="fetchPokemon(query), showLoader()" class="fa-solid text-purple-700 cursor-pointer bg-slate-200 p-6 border rounded-r-sm fa-magnifying-glass"></i>

            </div>
            
            <!-- history -->
            <div class="history absolute left-0  min-h-fit max-h-[250px] overflow-x-scroll top-full hidden group-focus-within:block rounded-b-md bg-slate-100/50 backdrop-blur-lg">
                <p v-if="history.length == 0" class="text-center py-4 w-full text-slate-500">
                    La tua cronologia apparirà qui
                </p>

                <!-- search history -->
                <ul v-if="history.length > 0" class="flex flex-col justify-center p-4  divide-y divide-slate-200 ">
                    <li v-for="(search, i) in history" class="py-2" :key="i" @click="console.log('click')">
                        <p class="text-slate-500 cursor-pointer">
                            {{ search }}
                        </p>
                    </li>
                </ul>
            </div>
        </div>

        <p v-if="error === 404" class="text-center text-4xl text-slate-400 py-12">
            Nessun Pokemon trovato :(
        </p>

        <p v-if="loading" class="text-center text-2xl font-slate-300">
            Cercando Pokemon
        </p>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {

        data(){
            return {
                query: '',
                error: null,
                loading: false,
                history: []
            }
        },

        props:{
            text: {
                type: String,
                required: true,
                default: 'Cerca un Pokemon'
            },
            
            pokedex: Array
        },

        methods:{
            fetchPokemon(poke){

                axios.get( `https://pokeapi.co/api/v2/pokemon/${poke.toLowerCase()}`) 
                    .then(res => {
                        this.$emit('onPokeRes', res)
                        this.history.push(this.query)
                        this.history = this.history.reverse()

                        this.query = ''

                        this.loading = false
                        const { status } = res
                        this.error = status

                        
                    })
                    .catch(err => {
                        const {status} = err.response
                        this.error = status

                        this.loading = false
                    })
            },

            showLoader(){
                this.loading = true
            },
        },

        mounted(){

        }
    }
</script>

<style lang="scss" scoped>
    .history{
        right: calc(0px + 62px);
    }
</style>