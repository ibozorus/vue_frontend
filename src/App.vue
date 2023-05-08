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
            activeComp: 'login',
            benutzername: null
        }
    },
    created() {
    },
    methods: {
        onClickChild(value) {
            this.activeComp = value;
        },
        setBenutzername(benutzername) {
            this.benutzername = benutzername;
            console.log(this.benutzername);
        },
        showAbmelden() {
            if (this.activeComp === "login" || this.activeComp === "register") {
                return false;
            } else {
                return true;
            }
        },
        abmelden() {
            localStorage.removeItem("benutzerId");
            this.onClickChild("login");
            this.benutzername = null;

        }
    }
}
</script>
<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">


        <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
                <a class="nav-link" v-show="showAbmelden()" @click="abmelden()">Abmelden <span
                        class="sr-only"></span></a>
            </li>
            <li class="nav-item active">
                <a class="nav-link" v-if="benutzername != null">{{ this.benutzername }} <span
                        class="sr-only"></span></a>
            </li>
        </ul>
    </nav>
    <div>
        <component @set-benutzername="setBenutzername" @clicked="onClickChild" :is="activeComp"></component>
    </div>
</template>
<style>
a:hover {
    cursor: pointer;
}
</style>
