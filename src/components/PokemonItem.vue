<template>
  <div class="card">
    <div class="card-body">
      <div class="text-center">
        <h2 class="card-title">{{ pokemon.name }}</h2>
        <p class="card-text">N.° {{ pokemon.id }}</p>
        <img v-bind:src="pokemon.sprites.other['official-artwork'].front_default" class="img-fluid" id="img-poke"/>
      </div>
      <div class="text-center">
        <button
          class="btn btn-success btn-md mt-4"
          data-bs-toggle="modal"
          data-bs-target="#poke-modal"
          @click="$emit('openModal', pokemon)"
        >
          Ver Pokemon
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PokemonItem',
  props: ['pokemon']
}
</script>

<style>
.card {
  height: 370px;
  margin: 1rem;
  border-radius: 5%;
  box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.3);
}

.card-text {
  color: #ccc;
  font-size: 20px;
}

.card-title {
  text-transform: uppercase;
}

#img-poke {
  height: 150px;
  /* border-radius: 50%;
  border: 1px solid black; */
}

.card-footer {
  margin-top: 20px;
}
</style>