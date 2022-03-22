<template>
  <div id="vertical-navbar">
    <div id="info">
      <h1 id="app-title"><a href="#"><span id="title-letters">Poke</span>dex</a></h1>
      <img src="../assets/profile1.jpg" id="profile-image"/>
      <h3 id="username">Username</h3>
      <h4 id="level">Level</h4>
      <p>Algunos datos relevantes mas</p>
    </div>
    <div id="logout">
      <button id="logout-btn">Cerrar sesión</button>
    </div>
  </div> 
</template>

<script>
export default {
  name: 'NavbarComponent'
}
</script>

<style>
  #vertical-navbar {
    min-width: 17rem;
    width: 17rem;
    height: 100vh;
    background: #5B7DB1;
    color: #fff;
    position: fixed;
    top: 0;
    left: 0;
    box-shadow: 3px 3px 10px rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: space-between;
    flex-direction: column;
    padding: 2rem;
  }

  #app-title a {
    text-decoration: none;
    color: #fff;
  }

  #app-title {
    color: #fff;
    text-transform: uppercase;
  }

  #title-letters {
    color: yellow;
    font-size: 120%;
    text-decoration: solid;
    text-shadow: 2px 1px 2px black;
  }

  #profile-image {
    width: 100%;
    border-radius: 50%;
    border: solid rgba(255,255,255, 0.3) 8px;
  }

  #info {
    text-align: center;
  }

  #level {
    color: rgba(255,255,255, 0.3);
  }

  #logout-btn {
    border: none;
    text-decoration: none;
    border-radius: 10px;
    padding: 10px;
    width: 100%;
    color: #fff;
    background-color: rgba(255,255,255, 0.3);
    font-size: 1.2rem;
  }

  @media (max-width: 768px) {
    #vertical-navbar {
      margin-left: -17rem;
    }
    #vertical-navbar.active {
      margin-left: 0;
    }
  }
</style>