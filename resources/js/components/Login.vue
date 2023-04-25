<template>
    <div class="w-50 m-auto">
        <input v-model="email" type="email" class="form-control mb-3 mt-3" placeholder="Enter Email">
        <input v-model="password" type="password" class="form-control mb-3" placeholder="Enter Password">
        <input @click.prevent="login" type="submit" class="btn btn-primary form-control" value="Log In">
    </div>
</template>

<script>
export default {
    name: "Login",

    data() {
        return {
            email: null,
            password: null,
        }
    },
    methods: {
        login() {
            axios.get('/sanctum/csrf-cookie')
                .then(response => {
                    axios.post('/login', {
                        email: this.email,
                        password: this.password
                    })
                        .then(response => {
                            //console.log(response.config.headers['X-XSRF-TOKEN']);
                            localStorage.setItem('x_xsrf_token', response.config.headers['X-XSRF-TOKEN'])
                            this.$router.push({ name: 'user.personal'})
                        })
                        .catch(error => {
                            console.log(error.response);
                        })
                })
        },
    }
}
</script>

<style scoped>

</style>
