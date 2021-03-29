<template> 
  <div class="home">
    <transition name="show">
        <img class="home-carousel" :src="`${imgscarousel[`${img}`]})`" :key="`${imgscarousel[`${img}`]})`" data-toggle="tooltip" data-placement="bottom" title="goTop" alt="">
    </transition>
     <div class="info-home">
        <h2 id="title">Encontre o carro ideal e <br> compre agora mesmo!</h2>
        <p class="subtitle">Ornare malesuada praesent aliquam varius mollis feugiat faucibus tristique ac aliquam, integer aenean commodo donec neque proin lacinia phasellus eget dui,<br> pulvinar auctor sapien nisl pretium curabitur eros donec per. </p>
      </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data(){
    return {
      imgscarousel:[
        'https://quatrorodas.abril.com.br/wp-content/uploads/2017/01/qr-690-carro-tracker-02.jpg?quality=70&strip=all',
        'https://quatrorodas.abril.com.br/wp-content/uploads/2020/03/chevrolet-tracker-premier-1.2-2021-1-e1597083614688.jpg?quality=70&strip=info',
        'https://2.bp.blogspot.com/-Rrkzkf-39Rw/We8n4kf8xKI/AAAAAAAA_mM/ROYZtJAYazQrQTzdVnQQNdw1_U5ZV-mawCLcBGAs/s1600/Tracker-premier-4.jpg',
        'https://www.moura.com.br/wp-content/uploads/2017/02/chevrolet-prisma-m48fd-1.jpg',
        'https://quatrorodas.abril.com.br/wp-content/uploads/2020/04/fiat-strada-endurance-2020-5.jpg?quality=70&strip=info'
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
    }, 4000)
  } 
};
</script>
<style scoped>
/*------------HOME-MAIN-------------*/
.home{
  height: 100vh;
  z-index: 2;
  overflow: hidden !important;
}
.home-carousel{
  height: 100vh;
  padding: 0;
  margin: 0;
  position: absolute;
  width: 100vw;
  z-index: 2;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  display: flex;
  justify-content: center;
  align-items: center;
}
@media(max-width: 500px) {
  #title{
    font-size: 1.6rem !important;
  }
  .subtitle{
    margin-top: 6rem !important;
    max-width: 20rem !important;
  }
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
  margin-top: 3rem;
  letter-spacing: .1rem;
  max-width: 30rem;
  text-align: start !important;
  font-weight: 400;
}
.info-home{
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  z-index: 2;
}
/* Show animation */
.show-enter-active,
.show-leave-enter {
  transform: translateX(0);
  transition: all .3s linear;
}
.show-enter,
.show-leave-to {
  transform: translateX(100%);
}

</style>