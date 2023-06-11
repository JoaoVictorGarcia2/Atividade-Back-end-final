<template>
     <h2>Atualizar Usuario</h2>
    <div class="container">
        <form @submit.prevent="update">
            <div>
                <label>e-mail; </label>
                <input type="email" v-model="email"></div>
            <div>
                <label>nome: </label>
                <input type="text" v-model="nome"></div>    
            <div>
                <label>senha: </label>
                <input type="password" v-model="senha"></div> <br>
            <button type="submit">Atualizar</button>
        </form>
        <p> {{ message }}</p>
    </div>
</template>
<script>
export default {
    data() {
        return {
            nome: '',
            email: '',
            senha: '',
            message: ''
        }
    },
    methods: {
        update(){
            const data = {
                nome: this.nome,
                email: this.email,
                senha: this.senha
            }
            fetch("http://localhost:8080/api/update", {
                method:"POST",
                headers: {'Content-Type': 'application/json'},
                body: JSON.stringify(data)
            })
            .then(async (res) => {
                this.message = await res.text();
            })
            .catch(async (err) =>{
                this.message = await err.text();
            })
        }
    }
}
</script>