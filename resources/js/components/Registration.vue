<template>
    <div class="w-50 m-auto">
        <input v-model="name" type="text" class="form-control mb-3 mt-3" placeholder="Enter name">
        <input v-model="email" type="email" class="form-control mb-3" placeholder="Enter Email">
        <input v-model="password" type="password" class="form-control mb-3" placeholder="Enter Password">
        <input v-model="password_confirmation" type="password" class="form-control mb-3" placeholder="Confirm Password">
        <input @click.prevent="register" type="submit" class="btn btn-primary form-control" value="Register">
    </div>
</template>

<script>
export default {
    name: "Registration",
    data() {
        return {
            name: null,
            email: null,
            password: null,
            password_confirmation: null,
        }
    },

    methods: {
        register() {
            axios.get('/sanctum/csrf-cookie')
                .then(response => {
                    axios.post('/register', {
                        name: this.name,
                        email: this.email,
                        password: this.password,
                        password_confirmation: this.password_confirmation
                    })
                        .then(response => {
                            //console.log(response);
                            localStorage.setItem('x_xsrf_token', response.config.headers['X-XSRF-TOKEN'])
                            this.$router.push({ name: 'user.personal'})

                        })
                        .catch(error => {
                            console.log(error.response);
                        })
                })
        }
    }
}
</script>

<style scoped>

</style>
