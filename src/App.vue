<script>

import Login from './components/LoginPage.vue'
import Register from './components/RegisterPage.vue'

export default {

    components: {
        "login": Login,
        "register": Register
    },
    data() {
        return {
            activeComp: 'login'
        }
    },
    created() {
    },
    methods: {}
}
</script>
<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">


        <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
                <a class="nav-link" @click="activeComp = 'login'">Login <span class="sr-only"></span></a>
            </li>
            <li class="nav-item active">
                <a class="nav-link" @click="activeComp = 'register'">Register <span class="sr-only"></span></a>
            </li>
        </ul>
    </nav>
    <div>
        <component :is="activeComp"></component>
    </div>
</template>
<style>
a:hover {
    cursor: pointer;
}
</style>
