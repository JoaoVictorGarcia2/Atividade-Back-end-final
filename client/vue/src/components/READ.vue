<template>
    <h2>Buscar Usuarios</h2> 
    <div class="container">
        <form @submit.prevent="read">
            <button type="submit">Ver todos</button>
            <p>{{ msg }}</p>
        </form>
        <ul v-if="users.length">
            <li v-for="user in users" :key="user.id">{{ user.nome }} - {{ user.email }}</li>
        </ul>
    </div>
    <br>
</template>
<script>
export default {
    data() {
        return {
            msg: '',
            users: []
        }
    },
    methods: {
        async read() {
            try {
                const response = await fetch('http://localhost:8080/api/read');
                const data = await response.json();
                this.users = data;
            } catch (error) {
                this.msg = error.message;
            }
        }
    },
}
</script>
<style scoped>
ul li {
    list-style: none;
}
</style>