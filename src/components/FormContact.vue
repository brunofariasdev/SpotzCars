<template>
    <div class="container">
        <input v-model="name" type="text">
        <input v-model="cpf" type="text">
        <input v-model="email" type="text">
        <input v-model="cell" type="text">
        <div class="buttons">
            <button>Enviar</button>
            <button>Cancelar</button>
        </div>
    </div>
</template>

<script>
export default {
    props:['name','cpf','email','cell'],
    data(){
        return{
            name: '',
            cpf: '', 
            email: '',
            cell:'',
            sent: null
        }
    }
}
</script>