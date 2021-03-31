<template>
    <main class="container">
      <form class="form-contact" @submit.prevent="sendForm()"  v-if="activeForm" required>
        <input type="text" placeholder="Nome" v-model="contactForm.name" required>
        <input type="text" pattern="^\d{2}\d{9}$" placeholder="CPF" v-model="contactForm.cpf" required>
        <input type="email" placeholder="Email"  title="Email Incorreto" v-model="contactForm.email" required>
        <input type="tel" pattern="^\d{2}\d{9}$" placeholder="Celular" v-model="contactForm.phone" required>
        <span v-if="form_sucess" class="form-sucess">Formulário de Contato ENVIADO!</span>
        <span v-if="form_error" class="form-error">Erro ao Enviar Formulário!</span>
        <div class="buttons">
          <button class="btn-sucess" type="submit">Enviar</button>
          <button class="btn-cancel"  @click="activeForm = false">Cancelar</button>
        </div>
      </form>
        <div class="search">
            <div class="price">
                <div class="filter-price">
                    <input v-model="minPrice" type="text" class="input-search" placeholder="Preço Mínimo">
                    <input v-model="maxPrice" type="text" class="input-search" placeholder="Preço Máximo">
                </div>
            </div>
            <div class="km">
                <div class="filter-km">
                    <input v-model="minKm"  type="text" class="input-search" placeholder="KM Mínimo">
                    <input v-model="maxKm"  type="text" class="input-search" placeholder="KM Máximo">
                </div>
            </div>
        <button class="button-search" @click="getCars()"><i class="fas fa-search"></i></button>
        </div>

        <div class="cards" v-if="search">
            <div class="card" v-for="cars in apiSearch" :key="cars.id">
                <img :src="getUrlImg(cars.image)">
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
          <img :src="getUrlImg(cars.image)">
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
            form_sucess: false,
            form_error: false,
            cars: [],
            search: false,
            activeForm: false
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
        getInContact(){
          this.activeForm = true;
        },
        sendForm(){
          let bodyPost = {
            "announcement_id": "string",
            "contact": {
              "name": this.contactForm.name,
              "cpf": this.contactForm.cpf,
              "email": this.contactForm.email,
              "phone": this.contactForm.phone
            }
          }
          axios.post('https://us-central1-spotz-prod.cloudfunctions.net/function-sell-my-car/contact', {
            bodyPost
          }).then(res => {
            console.log(res);
            this.form_sucess  = true;
            setTimeout(() => {this.form_sucess = false},3000)
            setTimeout(() => {this.activeForm = false},5000)
          }).catch(err => {
            console.log(err);
            this.form_error = true;
            setTimeout(() => {this.form_error = false},3000)
          });
        },
    },
  computed: {
    MaxKm: function(){
      if(this.maxKm !== ''){
      return '&maxKm='+this.maxKm;
      }else{
        return '';
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
  align-items: center;
  flex-direction: column;
  justify-content: center;
  background-image: url('https://demo.vehica.com/wp-content/uploads/2020/10/bg-1920-new.jpg');
  overflow: hidden;
}
.search-mb{
  display: none;
  flex-direction: row;
  margin-top:4rem;
}
.content-card{
  width: 100%;
}
.search{
  margin: 4rem 0rem 2rem 0;
  border-radius: 2rem;
  background-color: white;
  align-items: center;
  justify-content: center;
  display: flex;
  width: 70vw;
  padding: .3rem;
  box-shadow: 0px 5px 0px 0px #a1a1a1;
}
@media(max-width: 500px){
  .search-mb{
    align-items: center;
    display: flex;
    flex-direction: column;
  }
  .container{
    flex-direction: column;
  }
  .cards{
    margin: 0 !important;
  }
}
@media(max-width: 920px){
  .search{
    justify-content: center;
    width: 25rem;
    flex-direction: column;
  }
  .price, .km{
    width: 20rem;
    margin: 0;
    padding: 0;
  }

}
@media(max-width: 420px){
  .search{
    width: 21rem;
    height: 10rem;
    border-radius: 1.2rem;
  }
}
.content-search{
  display: flex;
  flex-direction: row;
}
.input-search{
  margin: .4rem;
  color: rgb(80, 79, 79);
  width: 40%;
}
.button-search{
  text-align: center;
  height: 3rem;
  color: rgb(255, 255, 255);
  font-size: 1rem;
  font-weight: bold;
  margin: .7rem;
  border-radius: 1rem;
  width: 5rem;
  background: var(--orange) !important;
  border: none;
  cursor: pointer;
}
.button-search:hover{
  background-color: var(--orange) !important;
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
  margin-bottom: .3rem;
  max-height: 85vh;
  justify-content: center;
}
.card{
  background-color: var(--black-contrast);
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
  color: var(--blue);
}
.price-km{
  padding: .3rem;
  display: flex;
  flex-direction: row;
  width: 90%;
  justify-content: space-between;
}
.price-km h2{
  color: var(--orange);
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
  background: var(--orange);
}
.btn-contact:hover{
  background: var(--orange-hover);
}
.form-contact{
  background: var(--black);
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
.form-contact input{
  width: 55vw;
  height: 2rem;
}
.btn-sucess{
  background-color: #2f9734;
  color: white;
  border: none;
  padding: .7rem;
  border-radius: .3rem;
  margin: .7rem;
  cursor: pointer;
  width: 8rem;
}
.btn-sucess:hover,.btn-cancel:hover{
  opacity: .8;
}
.btn-cancel{
  background-color: red;
  color: white;
  border: none;
  padding: .7rem;
  border-radius: .3rem;
  margin: .7rem;
  cursor: pointer;
  width: 8rem;
}
.form-sucess{
  color: #2f9734;
  padding: .2rem;
  font-size: 1.1rem;
}
.form-error{
  color: #cf0f0f;
  padding: .2rem;
  font-size: 1.1rem;
}
</style>