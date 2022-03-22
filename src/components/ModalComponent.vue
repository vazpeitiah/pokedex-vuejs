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
            <h5 class="modal-title fw-bold">Tarjeta Pokemon</h5>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body p-4">
            <div class="row">
              <div class="col-md-5 rounded" style="background: #eee">
                <img
                  v-bind:src="pokemon.sprites && pokemon.sprites.other['official-artwork'].front_default"
                  class="img-fluid"
                />
              </div>
              <div class="col-md-7 text-start">
                <h4 id="poke-name" class="fw-bolder">{{ pokemon.name }}</h4>
                <div class="d-flex justify-content-start">
                  <h6 id="poke-id" class="me-2">N.° {{ pokemon.id }}</h6>
                  <span v-for="type in pokemon.types" :key="type.slot" class="border rounded p-1 me-2" v-bind:class="type.type.name">
                    {{ type.type.name }}
                  </span>
                </div>
                
                <p>{{pokemon.specie ? pokemon.specie.flavor_text_entries[1].flavor_text : ''}}</p>
                <div id="info-poke" v-bind:class="pokemon.types && pokemon.types[0].type.name" >
                  <p><b>Altura:</b> {{ pokemon.height }} m</p>
                  <p><b>Peso:</b> {{ pokemon.weight }} kg</p>
                  <p><b>Experiencia base:</b> {{ pokemon.base_experience }}</p>
                  <p><b>Orden:</b> {{ pokemon.order }}</p>
                </div>
              </div>
            </div>
            <h5 class="fw-bold mt-2">Estadísticas</h5>
            <hr/>
            <div class="row mt-2">
              <div v-for="(stat, index) in pokemon.stats" :key="index" class="col-md-6">
                <div class="d-flex justify-content-between">
                  <span>{{stat.stat.name}}</span>
                  <span>{{stat.base_stat}}</span>
                </div>
                <div class="progress mb-2">
                  <div class="progress-bar"
                      v-bind:class="pokemon.types[0].type.name" 
                      role="progressbar" 
                      v-bind:style="`width: ${stat.base_stat}%;`" 
                      v-bind:aria-valuenow="stat.base_stat" 
                      aria-valuemin="0" 
                      aria-valuemax="150">
                  </div>
                </div>
              </div>
            </div>

            <h5 class="fw-bold mt-2">Evoluciones</h5>
            <hr/>
            <div id="evolutions" class="row">
              <div class="col-md-4">
                <p>{{pokemon.evolution_chain ? pokemon.evolution_chain.chain.species.name : ''}}</p>
                <img v-bind:src="pokemon.evolution_sprites && pokemon.evolution_sprites[0]" alt="" class="img-fluid"/>
              </div>
              <div class="col-md-4">
                <p>
                  {{ (pokemon.evolution_chain && pokemon.evolution_chain.chain.evolves_to.length > 0) ?  
                    pokemon.evolution_chain.chain.evolves_to[0].species.name : ''
                  }}
                </p>
                <img v-bind:src="pokemon.evolution_sprites && pokemon.evolution_sprites[1]" alt="" class="img-fluid"/>
              </div>
              <div class="col-md-4">
                <p>
                  {{ (pokemon.evolution_chain && pokemon.evolution_chain.chain.evolves_to.length > 0 && pokemon.evolution_chain.chain.evolves_to[0].evolves_to.length > 0) ?  
                    pokemon.evolution_chain.chain.evolves_to[0].evolves_to[0].species.name : ''
                  }}
                </p>
                <img v-bind:src="pokemon.evolution_sprites && pokemon.evolution_sprites[2]" alt="" class="img-fluid"/>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ModalComponent",
  props: ["pokemon"]
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
 /*  font-weight: bold; */
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

#evolutions p {
  color: #000;
  text-transform: uppercase;
}

#evolutions .col-md-4 {
  padding: 0.8rem;
  text-align: center;
  /* background-color: #eeeeee; */
}

#evolutions img {
  border-radius: 50%;
  border: 1px solid black;
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