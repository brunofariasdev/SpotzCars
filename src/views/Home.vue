<template> 
  <div class="home">
    <transition name="fade">
    <div class="home-carousel" :style="`background-image:url(${imgscarousel[`${img}`]})`" :key="`background-image:url(${imgscarousel[`${img}`]})`" data-toggle="tooltip" data-placement="bottom" title="goTop" alt="Background">
      <div class="info-home">
        <h2 id="title">Encontre o <span>Carro</span> ideal e <br> compre agora mesmo!</h2>
        <p class="subtitle">Ornare malesuada praesent aliquam varius mollis feugiat faucibus tristique ac aliquam, integer aenean commodo donec neque proin lacinia phasellus eget dui,<br> pulvinar auctor sapien nisl pretium curabitur eros donec per. </p>
      </div>
    </div>
    </transition>
    <footer>

    </footer>
  </div>  
</template>

<script>
export default {
  name: "Home",
  data(){
    return {
      imgscarousel:[
        'https://demo.vehica.com/wp-content/uploads/2020/10/bg-1920-new.jpg','https://images.unsplash.com/photo-1493238792000-8113da705763?ixlib=rb-1.2.1&ixid=MXwxMjA3fDB8MHxleHBsb3JlLWZlZWR8NXx8fGVufDB8fHw%3D&w=1000&q=80',
        'https://carrosecarros.com.br/upload/noticias/imagens/bYNMbV6kdb.jpg','https://cdn.motor1.com/images/mgl/rv6v6/s1/volkswagen-golf-8-gti-clubsport-2021.jpg','https://media2.autokopen.nl/afbeeldingen/volkswagen-golf-gti-tcr-295594-1920.jpg'
      ],
      img: 0, 
      cars: []
    }
  },
  created(){
    setInterval(() => {
      if(this.img < 4){
        this.img++;
      }else{
        this.img = 0;
      }
    },10000)
  } 
};
</script>
<style scoped>
/*------------HOME-MAIN-------------*/
.home{
  height: 100vh;
  z-index: 2;
}
.home-carousel{
  height: 100vh;
  z-index: 2;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  display: flex;
  justify-content: center;
  align-items: center;
}
.home-carousel:after{
  content: '\A';
  z-index: 2;
  position: absolute;
  width: 100%; height:100%;
  top:0; left:0;
  background:rgba(0, 0, 0, 0.349);
  opacity: 1;
}
#title{
  position: absolute;
  z-index: 3 !important;
  color: white;
  font-size: 2.5rem;
  letter-spacing: .1rem;
  text-align: start;
  font-weight: bold;
  margin-bottom: 12rem;
}
.subtitle{
  z-index: 3 !important;
  color: white;
  font-size: 1.2rem;
  margin-top: 10rem;
  letter-spacing: .1rem;
  max-width: 37rem;
  text-align: start !important;
  font-weight: 400;
}
.info-home{
  width: 62vw;
  display: flex;
  height: 100vh;
  justify-content: start;
  align-items: center;
}
.info-home span{
  color: var(--orange);
}
@media(max-width: 550px){
  #title{
    font-size:1.6rem;
  }
  .subtitle{
    margin-top: 8rem;
  }
}
@media(max-width: 415px){
  .subtitle{
    margin-top: 17rem;
  }
}
/* Fading animation */
.fade-enter-active,
.fade-leave-enter {
    transform: translateX(0);
    transition: all .3s linear;
}
.fade-enter,
.fade-leave-to {
    transform: translateX(100%);
}
</style>