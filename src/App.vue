<template>
  <div>
    <NavbarComponent />
    <ModalComponent v-bind:pokemon="selectedPokemon"/>
    <div id="main">
      <div id="header" class="d-flex justify-content-between">
        <div>
          <!-- <button class="btn border">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-list" viewBox="0 0 16 16">
              <path fill-rule="evenodd" d="M2.5 12a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5zm0-4a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5zm0-4a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5z"/>
            </svg>
            Menu
          </button> -->
        </div>
        <div>
          <div class="input-group">
            <input type="text" 
                   class="form-control"
                   placeholder="Buscar"
                   v-model="query"
                   @input="searchPokemon(query)"/>
            <span class="input-group-text text-light" style="background-color:#5B7DB1;">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-search" viewBox="0 0 16 16">
                <path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"/>
              </svg>
            </span>
          </div>
        </div>
      </div>
      <PokemonList :pokemons="copyPokemons" v-on:openModal="openModal" />
    </div>
  </div>
</template>

<script>
  import NavbarComponent from './components/NavbarComponent.vue'
  import PokemonList from './components/PokemonList.vue'
  import ModalComponent from './components/ModalComponent.vue'

  export default {
    name: 'App',
    components: {NavbarComponent, PokemonList, ModalComponent},
    data() {
      return {
        selectedPokemon: {},
        pokemonList: [],
        copyPokemons: [],
        query: ''
      }
    },
    methods: {
      openModal(pokemon) {
        //console.log(pokemon.name)
        this.selectedPokemon = {...pokemon}
      },
      searchPokemon(query){

        if(query.trim() === '') {
          this.copyPokemons = [...this.pokemonList]
        } else {
          const low = query.toLowerCase()
          const temp = this.pokemonList.filter(poke => {
            return poke.name.includes(low)
          })
          
          this.copyPokemons = [...temp]
        }
        
      }
    },
    mounted() {
      fetch('https://pokeapi.co/api/v2/pokemon?limit=120').then((res) => {
        return res.json()
      }).then((info) => {
        for(let index = 0; index < info.results.length; index++) {
          fetch(info.results[index].url).then((res2) => {
            return res2.json()
          }).then((poke) => {
            fetch('https://pokeapi.co/api/v2/pokemon-species/' + poke.id)
              .then( (res3) => {
                return res3.json()
              }).then((specie) => {
                poke = {...poke, specie}
                fetch(specie.evolution_chain.url)
                .then((res4) => {
                  return res4.json()
                })
                .then((ev) => {
                  poke = {...poke, evolution_chain: ev}
                  this.pokemonList.push(poke)
                  this.copyPokemons.push(poke)
                })
              })
          })
        }
      })
    }
  }

</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');

  * {
    font-family: 'Montserrat', sans-serif;
  }
  #main {
    width: calc(100% - 17rem);
    margin-left: 17rem;
    padding: 2rem;
  }

  @media (max-width: 768px) {
    #main {
      width: 100%;
      margin: 0;
    }
    #main.active {
      margin-left: 17rem;
      width: calc(100% - 17rem);
    }
  }
</style>
