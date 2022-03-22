<template>
  <div>
    <NavbarComponent v-on:searchPokemon="searchPokemon"/>
    <ModalComponent v-bind:pokemon="selectedPokemon"/>
    <div id="main" class="container">
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

  /* #main {
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
  } */
</style>
