<template>
    <div>
        <ul class="nav nav-pills nav-fill mb-3">
            <li v-if="token" class="nav-item btn btn-info m-1">
                <router-link  :to="{ name: 'get.index' }" class="nav-link text-dark">Get</router-link>
            </li>
            <li v-if="token" class="nav-item btn btn-info m-1">
                <router-link :to="{ name: 'user.personal' }" class="nav-link text-dark">Personal</router-link>
            </li>
            <li v-if="!token" class="nav-item btn btn-info m-1">
                <router-link :to="{ name: 'user.login' }" class="nav-link text-dark">Login</router-link>
            </li>
            <li v-if="!token" class="nav-item btn btn-info m-1">
                <router-link :to="{ name: 'user.registration' }" class="nav-link text-dark">Sign Up</router-link>
            </li>
            <li v-if="token" @click.prevent="logout" class="nav-item btn btn-info m-1">
                <a href="#" class="nav-link text-dark">LogOut</a>
            </li>
        </ul>
        <router-view></router-view>
    </div>
</template>

<script>
export default {
    name: "Index",
    data() {
        return {
            token: null,
        }
    },
    mounted() {
        this.getToken()
    },
    updated() {
        this.getToken()

    },
    methods: {
        getToken(){
            this.token = localStorage.getItem('x_xsrf_token')
        },
        logout() {
            axios.post('/logout')
            .then( response => {
                localStorage.removeItem('x-xsrf-token')
                this.$router.push({ name: 'user.login'})
            })
        }
    }
}
</script>

<style scoped>

</style>
