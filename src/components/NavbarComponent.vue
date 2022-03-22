<template>
<nav class="navbar navbar-expand-lg navbar-dark">
  <div class="container-fluid">
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarTogglerDemo03" aria-controls="navbarTogglerDemo03" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <a class="navbar-brand" href="/">
      <img src="../assets/favicon-32x32.png" alt="" width="32" height="32" class="d-inline-block align-text-top">
      Pokedex
    </a>
    <div class="collapse navbar-collapse" id="navbarTogglerDemo03">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li class="nav-item">
          <a class="nav-link active" aria-current="page" href="/">Incio</a>
        </li>
      </ul>
      <form class="d-flex">
        <input class="form-control me-2" 
               type="search" 
               placeholder="Buscar" 
               aria-label="Search"
               v-model="query"
               v-on:input="$emit('searchPokemon', query)">
        <!-- <button class="btn btn-outline-primary" type="submit"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-search" viewBox="0 0 16 16">
                <path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"/>
              </svg></button> -->
      </form>
    </div>
  </div>
</nav>
</template>

<script>
export default {
  name: 'NavbarComponent',
  data() {
    return {
      query: ''
    }
  }  
}
</script>

<style>
.navbar {
  background-color: #5B7DB1;
}

</style>