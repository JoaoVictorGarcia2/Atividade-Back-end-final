<template>
    <h2>Cadastro de Usuario</h2>
    <div class="container">
        <form @submit.prevent="create">
            <div>
                <label>nome: </label>
                <input type="text" v-model="nome"/></div>
            <div>
                <label>email: </label>
                <input type="email" v-model="email"/></div>
            <div>
                <label>senha: </label>
                <input type="password" v-model="senha"/></div><br>
            <button type="submit">Enviar</button>
        </form>
        <p>{{ message }}</p>
    </div> <br>
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
            create(){
                const data = {
                    nome: this.nome,
                    email: this.email,
                    senha: this.senha
                }
                console.log(data);
                fetch('http://localhost:8080/api/create', {
                    method: 'POST',
                    headers: {'Content-Type': 'application/json'},
                    body: JSON.stringify(data)
                })
                .then(async (res) => {
                        this.message = await res.text();
                })
                .catch(async (error) => {
                        this.message = error.message;
                })
            }  
        },
    }
</script>