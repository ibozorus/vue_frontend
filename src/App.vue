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
        sessionStorage.clear();
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
            sessionStorage.removeItem("benutzerId");
            this.onClickChild("login");
            this.benutzername = null;

        },
        async createNewBoard() {
            let body = {
                "text": "Board",
                "benutzer": {
                    "id": sessionStorage.getItem("benutzerId")
                }
            }
            await fetch("http://localhost:8081/api/v1/board", {
                method: "POST",
                body: JSON.stringify(body),
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                }

            }).then((response) => {
                response.json().then((data) => {
                    console.log(data);
                })
            })
        }
    }
}
</script>
<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">


        <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
                <a class="nav-link" v-if="benutzername != null">{{ this.benutzername }} <span
                        class="sr-only"></span></a>
            </li>
            <li class="nav-item active">
                <a class="nav-link" v-show="showAbmelden()" @click="abmelden()">Abmelden <span
                        class="sr-only"></span></a>
            </li>
            <li class="nav-item active">
                <a class="nav-link" v-show="this.activeComp === 'boards'" @click="createNewBoard()">Create new
                    board!!!!!<span
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
