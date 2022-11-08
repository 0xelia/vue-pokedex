<template>
    <div class="container mt-8 mb-4 h-52">
        <h2 class="text-xl">
            Il tuo Pokedex
            <span v-if="pokedex.length > 0"> ({{pokedex.length}}) </span>
        </h2>

        <div v-if="pokedex.length == 0" class="h-full flex justify-content items-center text-slate-500">
            <p class="w-full text-bold text-2xl text-center">
                Il tuo pokedex è vuoto
            </p>
        </div>

        <ul class="flex gap-8 w-full overflow-y-scroll">
            <li v-for="pokemon in pokedex" :key="pokemon.id" class="flex flex-col animate__animated animate__backInUp">
                <p class="text-center text-lg text-slate-500 capitalize">
                    {{pokemon.name}}
                </p>
                <figure class="flex justify-center">
                    <img :src="pokemon.sprites.front_default" alt="">
                </figure>
                <div class="flex gap-2">
                    <button @click="$emit('onPokeClick', {pokemon, show: true})" class="py-2 px-4 text-white bg-purple-700 rounded">Mostra</button>
                    <button @click="$emit('onPokeClick', {pokemon, remove: true})" class="py-2 px-4 text-purple-700 border rounded border-purple-700">Elimina</button>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        props: {
            pokedex: Array,
        },        
    }
</script>

<style lang="scss" scoped>
</style>