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
        <a class="navbar-brand" href="#">Navbar</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
                aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
                <li class="nav-item active">
                    <a class="nav-link" @click="activeComp = 'login'">Login <span class="sr-only"></span></a>
                </li>
                <li class="nav-item active">
                    <a class="nav-link" @click="activeComp = 'register'">Register <span class="sr-only"></span></a>
                </li>
            </ul>
        </div>
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
