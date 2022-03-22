<template>
  <div class="cards row">
    <div class="col-md-4" v-for="pokemon in pokemons" :key="pokemon.id">
      <PokemonItem v-bind:pokemon="pokemon" v-on:openModal="$emit('openModal', pokemon)"/>
    </div>
  </div>
</template>

<script>
import PokemonItem from './PokemonItem.vue'

export default {
  name: 'PokemonList',
  props: ['pokemons'],
  components: {PokemonItem}
};
</script>

<style>
</style>