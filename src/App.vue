<template>
  <div id="app">
    <div id="nav">
      <span>SpotzCars</span>
      <div class="menu">
        <router-link class="menu-item" to="/">Home</router-link> 
        <router-link class="menu-item" to="/about">Buscar</router-link>
        <router-link class="menu-item" to="/about">Sobre</router-link>
      </div>
    </div>
    <router-view id="view" />
  </div>
</template>

<style>
*{
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  height: 100vh;
  width: 100vw;
  overflow: hidden !important;
}
#view{
  overflow-x: auto;
}
#nav{
  overflow: hidden;
  background: transparent;
  position: fixed;
  top: 0;
  width: 100%;
  display: flex;
  flex-direction: row;
  height: 4rem;
  background-color:transparent;
}
.menu-item{
  color: red;
  text-decoration: none;
  padding: .3rem;
  font-size: 1.2rem;
}
</style>
