<template>
  <!-- Modal -->
  <div>
    <div
      class="modal fade"
      id="poke-modal"
      tabindex="-1"
      aria-labelledby="pokemodalLabel"
      aria-hidden="true">
      <div class="modal-dialog modal-lg">
        <div class="modal-content">
          <div class="modal-header">
            <h2 class="modal-title">Tarjeta Pokemon</h2>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body p-4">
            <div class="row">
              <div class="col-md-6 rounded" style="background: #eee">
                <img
                  v-bind:src="pokemon.sprites && pokemon.sprites.other['official-artwork'].front_default"
                  class="img-fluid"
                />
              </div>
              <div class="col-md-6 text-start">
                <h2 id="poke-name">{{ pokemon.name }}</h2>
                <h5 id="poke-id">N.° {{ pokemon.id }}</h5>
                <p>{{pokemon.specie ? pokemon.specie.flavor_text_entries[1].flavor_text : ''}}</p>
                <div id="info-poke" v-bind:class="pokemon.types && pokemon.types[0].type.name" >
                  <p><b>Altura:</b> {{ pokemon.height }}</p>
                  <p><b>Peso:</b> {{ pokemon.weight }}</p>
                  <p><b>Experiencia base:</b> {{ pokemon.base_experience }}</p>
                  <p><b>Orden:</b> {{ pokemon.order }}</p>
                </div>
                <h3>Tipo</h3>
                <div id="poke-types" class="d-flex">
                  <span v-for="type in pokemon.types" :key="type.slot" class="border" v-bind:class="type.type.name">
                    {{ type.type.name }}
                  </span>
                </div>
              </div>
            </div>
            <h3>Evoluciones</h3>
            <div id="evolutions" class="row">
              <div class="col-md-4 border bg-secondary">
                <p>{{pokemon.evolution_chain ? pokemon.evolution_chain.chain.species.name : ''}}</p>
                <img src="" alt="" class="img-fluid"/>
              </div>
              <div class="col-md-4 border bg-secondary">
                <p>
                  {{ (pokemon.evolution_chain && pokemon.evolution_chain.chain.evolves_to.length > 0) ?  
                    pokemon.evolution_chain.chain.evolves_to[0].species.name : ''
                  }}
                </p>
                <img src="" alt="" class="img-fluid"/>
              </div>
              <div class="col-md-4 border bg-secondary">
                <p>
                  {{ (pokemon.evolution_chain && pokemon.evolution_chain.chain.evolves_to.length > 0 && pokemon.evolution_chain.chain.evolves_to[0].evolves_to.length > 0) ?  
                    pokemon.evolution_chain.chain.evolves_to[0].evolves_to[0].species.name : ''
                  }}
                </p>
                <img src="" alt="" class="img-fluid"/>
              </div>
            </div>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Close
            </button>
            <!-- <button type="button" class="btn btn-primary">Save changes</button> -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ModalComponent",
  props: ["pokemon"],

};
</script>

<style>
.modal-title {
  text-transform: uppercase;
  text-align: center;
}

#info-poke {
  display: grid;
  grid-template-columns: 1fr 1fr;
  /* background-color: #5b7db1; */
  border-radius: 15px;
  padding: 1rem;
  font-weight: bold;
}

#info-poke p b {
  display: flex;
  /* color: #fff; */
}

#poke-name {
  text-transform: uppercase;
}

#poke-id {
  text-transform: uppercase;
  color: #ccc;
}

#poke-types {
  font-size: 1rem;
  text-transform: lowercase;
}

#poke-types span {
  padding: 5px;
  border-radius: 10px;
  margin-right: 5px;
}

#evolutions p {
  color: #fff;
  text-transform: uppercase;
}

#evolutions .col-md-4 {
  padding: 0.6rem;
}

.grass {
  background-color: #5d9067;
  color: #fff;
}

.poison {
  background-color: purple;
  color: #fff;
}

.fire {
  background-color: #dd533b;
  color: #fff;
}

.water {
  background-color: #8fc3d0;
  color: #fff;
}

.bug {
  background-color: #b08658;
  color: #fff;
}

.normal {
  background-color: #e7dca8;
}

.flying {
  background-color: thistle;
}

.ground {
  background-color: #7f5555;
  color: #fff;
}

.fairy {
  background-color: #d6aab3;
  color: #fff;
}

.electric {
  background-color: #f3d77c;
}

.rock {
  background-color: #abb4c5;
}

.fighting {
  background-color: tomato;
  color: #fff;
}

.psychic {
  background-color: #000;
  color: #fff;
}

</style>