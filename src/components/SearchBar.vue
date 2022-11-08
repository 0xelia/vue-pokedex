<template>
    <div class="container py-6">
        <h1 class="text-lg font-bold mb-4">
            {{text}}
        </h1>
        <div class="searchbar flex items-center">

            <input @keyup.enter="fetchPokemon(), showLoader()" class="border border-r-0 border-slate-300 rounded rounded-r-none w-full px-6 h-16" type="text" v-model="query" placeholder="es. Pikachu" name="query" id="">
            <i @click="fetchPokemon(), showLoader()" class="fa-solid text-purple-700 cursor-pointer bg-slate-200 p-6 border rounded-r-sm fa-magnifying-glass"></i>
            
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
                query: null,
                error: null,
                loading: false
            }
        },
        props:{
            text: {
                type: String,
                required: true,
                default: 'Cerca un Pokemon'
            }
        },

        methods:{
            fetchPokemon(){

                axios.get( `https://pokeapi.co/api/v2/pokemon/${this.query.toLowerCase()}`) 
                    .then(res => {
                        this.$emit('onPokeRes', res)

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

</style>