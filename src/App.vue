<template>
  <div id="app">
    <div class="nav">
      <div class="menu">
        <span>spotzCar<i class="fas fa-car"></i></span>
        <i @click="activemb()" :class="mbicon" id="mbicon"></i>
        <ul class="mndesk">
          <router-link class="itemdesk" to="/">Inicio</router-link>
          <router-link class="itemdesk" to="/about">Sobre</router-link>
          <router-link class="itemdesk" to="/search">Buscar</router-link>
        </ul>
      </div>
    </div>
    <div class="menuactive" :style="activemenu">
      <ul>
        <router-link class="itemmb" to="/">Inicio</router-link>
        <router-link class="itemmb" to="/about">Sobre</router-link>
        <router-link class="itemmb" to="/search">Buscar</router-link>
      </ul>
    </div>
    <router-view id="view"/>
  </div>
</template>

<script>
export default {
  data(){
    return {
      activemenu: '',
      mbicon:'fas fa-bars'
    }
  }, 
  methods:{
    activemb(){
      if(this.activemenu == ''){
        this.activemenu = 'display:block'
        this.mbicon = 'fas fa-times'
      }else{
        this.activemenu = ''
        this.mbicon = 'fas fa-bars'
      }
    }
  }
}
</script>

<style>
:root{
  --orange: #FF4605;
  --orange-hover: #ff6831;
  --black: #222732;
  --blue: #EFF3FA;
  --grey: #DEE1E6; 
  --black-contrast: #0f141e;
}
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
  overflow-x: hidden !important;
}
/*------------NAV-MB--------------*/
.nav{
  position: fixed;
  background: transparent;
  z-index: 3;
}
.menu{
  display: flex;
  background: transparent;
  position: fixed;
  height: 3rem;
  align-items: center;
  justify-content: space-around;
  width: 100vw;
  z-index: 3;
}
.menu span{
  color: white;
  font-weight: bold;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
  font-size: 1.3rem;
  z-index: 3;
  cursor: pointer;
}
.menu span i{
  font-size: 1.4em;
  padding: .3rem;
  color: var(--orange);  
  z-index: 3;
}
.menuactive{
  margin-top: 3rem;
  display: none;
  height: 100vh;
  width: 100vw;
  position: absolute;
  animation-name: animemenu;
  animation-duration: .8s;
  background-color: rgb(255, 255, 255);
  border-radius: 1rem 1rem 0 0;
  z-index: 3;
  position: fixed;
}
@keyframes animemenu{
  to{margin-top: 3rem;}
  from{margin-top: 80rem;}
}
.menuactive ul{
  margin-top: 2rem;
  display: flex;
  flex-direction: column;
  z-index: 3;
}
.itemmb{
  color: #47494bab;
  text-decoration: none;
  list-style: none;
  text-align: start;
  z-index: 3;
  font-size: 1.2rem;
  font-weight: 300;
  padding: .5rem; 
}
.mndesk{
  display: none;
  flex-direction: row;
}
.itemdesk{
  font-size: 1.2rem;
  color: white;
  padding: 0 .7rem;
  font-weight: bold;
  list-style: none;
  text-decoration: none;
  padding-top: .5rem;
}
.itemdesk:hover{
  color: var(--orange-hover);
  cursor: pointer;
}
#mbicon{
  font-size: 1.8rem;
  color: white;
  }
/*------------NavBar-MediaQuery--------------*/
@media(min-width: 600px){
  #mbicon{
    display: none;
  }
  .mndesk{
    display: flex;
  }
}
</style>
