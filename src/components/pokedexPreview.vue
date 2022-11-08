<template>
    <div class="container mt-8 mb-4 h-52">
        <h2 class="text-xl">
            Il tuo Pokedex
        </h2>
        <ul class="flex gap-8 w-full overflow-hidden">
            <li v-for="pokemon in pokedex" :key="pokemon.id" class="flex flex-col">
                <p class="text-center text-lg text-slate-500 capitalize">
                    {{pokemon.name}}
                </p>
                <figure class="flex justify-center">
                    <img :src="pokemon.sprites.front_default" alt="">
                </figure>
                <div class="flex gap-2">
                    <button @click="$emit('onPokeShow', pokemon)" class="py-2 px-4 text-white bg-purple-700 rounded">Mostra</button>
                    <button @click="$emit('onPokeRemove', pokemon)" class="py-2 px-4 text-purple-700 border rounded border-purple-700">Elimina</button>
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