<template>
    <main class="container">
        <div class="search">
            <div class="price">
                <span>Preço</span>
                <div class="filter-price">
                    <input type="text" class="input-search" placeholder="Preço Mínimo">
                    <input type="text" class="input-search" placeholder="Preço Máximo">
                </div>
            </div>
            <div class="km">
                <span>Quilometragem</span>
                <div class="filter-km">
                    <input type="text" class="input-search" placeholder="KM Mínimo">
                    <input type="text" class="input-search" placeholder="KM Máximo">
                </div>
            </div>
        <button class="button-search">Buscar</button>
        </div>

        <div class="cards">
            <div class="card" v-for="cars in api" :key="cars">
                <img :src="`../assets/img/${cars.image}`" alt="">
                <span>Nome: {{cars.name}}</span>
                {{cars.image}}
                <span>Marca: {{cars.brand}}</span>
                <div class="price-km">
                    <h2>R$: {{cars.price}}</h2>
                    <span>{{cars.km}} Km</span>
                </div>
                 <button class="btn-contact">Entrar em Contato</button>
            </div>
        </div>
    </main>
</template>
<script>
export default {
    data(){
        return{
            api: [], 
            urlApi: 'https://us-central1-spotz-prod.cloudfunctions.net/function-sell-my-car/announcements'
        }
    }, 

    created(){
        fetch(this.urlApi)
            .then(response => response.json())
            .then(card => {
                return this.api = card.cars
            })
    }
}
</script>
<style scoped>
.container{
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    flex-direction: row;
    justify-content: center;
    background: transparent linear-gradient(45deg,#e2835a,#af69be) 0 0 no-repeat padding-box;
    overflow: hidden;
}
.search{
    background-color: white;
    height: 93vh;
    width: 19rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 6rem;
    border-radius: .2rem;
    padding: 1rem 0 0 0 ;
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
    overflow-x: height;
    overflow-y: scroll ;
    max-height: 85vh;
    margin-top: 7rem;
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


</style>