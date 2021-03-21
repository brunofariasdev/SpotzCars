<template>
  <div class="home">
    <div class="home-carousel" :style="`background-image:url(${imgscarousel[`${img}`]})`">
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  data(){
    return {
      imgscarousel: [
        'https://images.unsplash.com/photo-1493238792000-8113da705763?ixlib=rb-1.2.1&ixid=MXwxMjA3fDB8MHxleHBsb3JlLWZlZWR8NXx8fGVufDB8fHw%3D&w=1000&q=80',
        'https://revistacarro.com.br/wp-content/uploads/2019/09/Ferrari-F8-Spider_3-1024x614.jpg','https://carrosecarros.com.br/upload/noticias/imagens/bYNMbV6kdb.jpg','https://cdn.motor1.com/images/mgl/rv6v6/s1/volkswagen-golf-8-gti-clubsport-2021.jpg'
      ],
      img: 0
    }
  },
  components: {
    
  },
  computed:{
    
    
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
}
.home-carousel:after {
    content: '\A';
    z-index: 2;
    position: absolute;
    width: 100%; height:100%;
    top:0; left:0;
    background:rgba(0, 0, 0, 0.349);
    opacity: 1;
}
</style>