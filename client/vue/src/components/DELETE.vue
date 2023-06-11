<template>
    <h2>Remover usuario</h2>
    <div class="container">
        <form @submit.prevent="delet">
            <div>
                <label>e-mail: </label>
                <input type="email" v-model="email"></div>   
            <div>
                <label>senha: </label>
                <input type="password" v-model="senha"></div><br>
            <button type="submit">Remover</button>
        </form>
        <p> {{ message }}</p>
    </div>
    <br>
</template>
<script>
export default {
    data() {
        return {
            email: '',
            senha: '',
            message: '',
        }
    },
    methods: {
        delet(){
            const data = {
                email: this.email,
                senha: this.senha
            }
            fetch("http://localhost:8080/api/delet", {
                method:"DELETE",
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