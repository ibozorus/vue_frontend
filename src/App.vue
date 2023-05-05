<script>

import Login from './components/LoginPage.vue'
import Register from './components/RegisterPage.vue'
import BoardsUebersicht from "@/components/BoardsUebersicht.vue";

export default {

    components: {
        "login": Login,
        "register": Register,
        "boards": BoardsUebersicht
    },
    data() {
        return {
            activeComp: 'login'
        }
    },
    created() {
    },
    methods: {
        onClickChild (value) {
            this.activeComp = value;
        }
    }
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
            <li class="nav-item active">
                <a class="nav-link disabled" @click="activeComp = 'boards'">Boards <span class="sr-only"></span></a>
            </li>
        </ul>
    </nav>
    <div>
        <component @clicked="onClickChild" :is="activeComp"></component>
    </div>
</template>
<style>
a:hover {
    cursor: pointer;
}
</style>
