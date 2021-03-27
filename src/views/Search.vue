<template>
    <main class="container">
      <form class="form-contact"  v-if="activeForm" required>
        <input type="text" placeholder="Nome" v-model="contactForm.name" required>
        <input type="text" pattern="^\d{2}\d{9}$" placeholder="CPF" v-model="contactForm.cpf" required>
        <span v-if="valCpf" >Cpf Invalido!</span>
        <input type="email" placeholder="Email"  title="Email Incorreto" v-model="contactForm.email" required>
        <input type="tel" pattern="^\d{2}\d{9}$" placeholder="Celular" v-model="contactForm.phone" required>
        <span v-if="valPhone">Telefone Invalido!</span>
        <div class="buttons">
          <button class="btn-sucess" type="submit" @click="sendForm()">Enviar</button>
          <button class="btn-cancel"  @click="activeForm = false">Cancelar</button>
        </div>
      </form>
        <div class="search">
            <div class="price">
                <span>Preço</span>
                <div class="filter-price">
                    <input v-model="minPrice" type="text" class="input-search" placeholder="Preço Mínimo">
                    <input v-model="maxPrice" type="text" class="input-search" placeholder="Preço Máximo">
                </div>
            </div>
            <div class="km">
                <span>Quilometragem</span>
                <div class="filter-km">
                    <input v-model="minKm"  type="text" class="input-search" placeholder="KM Mínimo">
                    <input v-model="maxKm"  type="text" class="input-search" placeholder="KM Máximo">
                </div>
            </div>
        <button class="button-search" @click="getCars()">Buscar</button>
        </div>
        <div class="search-mb">
          <div class="content-search">
            <div class="price">
              <span>Preço</span>
              <div class="filter-price">
                <input v-model="minPrice" type="text" class="input-search" placeholder="Preço Mínimo">
                <input v-model="maxPrice" type="text" class="input-search" placeholder="Preço Máximo">
              </div>
            </div>
            <div class="km">
              <span>Quilometragem</span>
              <div class="filter-km">
                <input v-model="minKm"  type="text" class="input-search" placeholder="KM Mínimo">
                <input v-model="maxKm"  type="text" class="input-search" placeholder="KM Máximo">
              </div>
            </div>
          </div>
          <button class="button-search" @click="getCars()">Buscar</button>
        </div>

        <div class="cards" v-if="search">
            <div class="card" v-for="cars in apiSearch" :key="cars.id">
                <img src="../assets/images/fghc453d.jpg">
                <div class="content-card">
                  <span>Nome: {{cars.name}}</span>
                  <span>Marca: {{cars.brand}}</span>
                  <div class="price-km">
                    <h2>R$: {{cars.price}}</h2>
                    <span>{{cars.km}} Km</span>
                  </div>
                  <button class="btn-contact" @click="getInContact(cars)">Entrar em Contato</button>
                </div>
            </div>
        </div>
      <div class="cards" v-else>
        <div class="card" v-for="cars in apiTotal" :key="cars.id">
          <img src="../assets/images/fghc453d.jpg">
          <span>Nome: {{cars.name}}</span>
          <span>Marca: {{cars.brand}}</span>
          <div class="price-km">
            <h2>R$: {{cars.price}}</h2>
            <span>{{cars.km}} Km</span>
          </div>
          <button class="btn-contact" @click="getInContact(cars)">Entrar em Contato</button>
        </div>
      </div>
    </main>
</template>
<script>
import axios from 'axios';
export default {
    data(){
        return{
            apiTotal: [],
            contactForm: {name: '', cpf: '',phone: '', email: ''},
            apiSearch:[],
            maxKm: '',
            minKm: '',
            maxPrice: '',
            minPrice: '',
            valCpf: false,
            valPhone: false,
            cars: [],
            search: false,
            activeForm: true
        }
    },
    mounted() {
      let baseUrl = 'https://us-central1-spotz-prod.cloudfunctions.net/function-sell-my-car/announcements?';
      axios.get(baseUrl)
        .then(res => {
          this.apiTotal = res.data.cars;
        })
    },
  methods:{
        getUrlImg(pic){
          return require(`../assets/images/${pic}`);
        },
        getCars(){
          this.search = true;
          let searchUrl = 'https://us-central1-spotz-prod.cloudfunctions.net/function-sell-my-car/announcements?'+this.MinPrice+this.MaxPrice+this.MaxKm+this.MinKm;;
            axios.get(searchUrl)
              .then(res => {
                this.apiSearch = res.data.cars;
                console.log(searchUrl);
              })
        },
        getInContact(e){
          this.activeForm = true;
          console.log(e.name, e.id, e.price, e.brand);
        },
        sendForm(){
          console.log(this.contactForm.name, this.contactForm.email, this.contactForm.phone, this.contactForm.cpf);
        },

    },
  computed: {
      MaxKm: function(){
          if(this.maxKm !== ''){
            return '&maxKm='+this.maxKm;
          }else{
            return ''
          }
      },
    MinKm: function(){
      if(this.minKm !== ''){
        return '&minKm='+this.minKm;
      }else{
        return ''
      }
    },
    MaxPrice: function(){
      if(this.maxPrice !== ''){
        return '&maxPrice='+this.maxPrice;
      }else{
        return ''
      }
    },
    MinPrice: function(){
      if(this.minPrice !== ''){
        return '&minPrice='+this.minPrice;
      }else{
        return ''
      }
    },
  },


}

</script>
<style scoped>
.container{
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: start;
    flex-direction: row;
    justify-content: center;
    background: transparent linear-gradient(45deg,#e2835a,#af69be) 0 0 no-repeat padding-box;
    overflow: hidden;
}
.search-mb{
  display: none;
  flex-direction: row;
  margin-top:4rem;
}
.search{
    background-color: white;
    height: 93vh;
    width: 19rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 4.2rem;
    border-radius: .2rem;
    padding: 1rem 0 0 0 ;
}

@media(max-width: 500px){
  .search-mb{
    align-items: center;
    display: flex;
    flex-direction: column;
  }
  .search{
    display: none;
  }
  .container{
    flex-direction: column;
  }
  .cards{
    margin: 0 !important;
  }
}
.content-search{
  display: flex;
  flex-direction: row;
}
.input-search{
    margin: .4rem;
    color: rgb(80, 79, 79);
    width: 80%;
}
.button-search{
    text-align: center;
    height: 2.3rem;
    color: white;
    font-size: 1rem;
    font-weight: bold;
    margin: 1rem;
    border-radius: 1rem;
    width: 10rem;
    background: transparent linear-gradient(45deg,#f16e34,#9940ac) 0 0 no-repeat padding-box;
    border: none;
    cursor: pointer;
}
.button-search:hover{
    background: transparent linear-gradient(45deg,#db622e,#873599) 0 0 no-repeat padding-box;
    font-size: 1.1rem;
}
.cards{
    width: 100%;
    margin-left: .8rem;
    display: flex;
    flex-wrap: wrap;
    flex-direction: row;
    overflow-x: hidden;
    overflow-y: scroll ;
    max-height: 85vh;
    margin-top: 4.2rem;
    justify-content: center;
}
.card{
    background-color: white;
    width: 16rem;
    border-radius: .4rem;
    margin-bottom: .4rem;
    display: flex;
    justify-content: space-between;
    align-items: start;
    flex-direction: column;
    margin-left: .4rem;
    height: 20rem;
    box-shadow: rgba(158, 184, 209, 0.41) 0px 2px 9px 0px;;
}
.card img{
    width: 100%;
    height: 11rem;
    border-radius: .4rem .4rem 0 0;
}
.card span{
    padding: .3rem;
}
.price-km{
    padding: .3rem;
    display: flex;
    flex-direction: row;
    width: 90%;
    justify-content: space-between;
}

.price-km h2{
    color: rgb(22, 21, 21);
    font-size: 1rem;
}
.price-km span{
    font-size: .8rem;
    color: rgb(158, 158, 158);
}
.btn-contact{
    border: none;
    width: 100%;
    height: 2.5rem;
    color: white;
    cursor: pointer;
    font-weight: 500;
    background: transparent linear-gradient(45deg,#65c86a,#17ac1e) 0 0 no-repeat padding-box;
}
.btn-contact:hover{
    background: transparent linear-gradient(45deg,#2f9734,rgb(17, 134, 23)) 0 0 no-repeat padding-box;
}
.form-contact{
  background: transparent linear-gradient(45deg,#e2835a,#af69be) 0 0 no-repeat padding-box;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-items: center;
  justify-content: center;
  z-index: 1;
  position: absolute;
}
.form-contact input{
  padding: .5rem;
  margin: .5rem;
}
.btn-sucess{
  background-color: #2f9734;
  color: white;
  border: none;
  padding: .7rem;
  border-radius: .3rem;
  margin: .7rem;
  cursor: pointer;
}
.btn-cancel{
  background-color: red;
  color: white;
  border: none;
  padding: .7rem;
  border-radius: .3rem;
  margin: .7rem;
  cursor: pointer;
}
</style>