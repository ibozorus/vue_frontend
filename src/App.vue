<script>
import {preventOverflow} from "@popperjs/core";

export default {
    data() {
        return {
            allBenutzer: [],
            benutzername: "",
            password: ""
        }
    },
    created() {
        this.fetchAllUsers();
    },
    methods: {
        async fetchAllUsers() {
            await fetch("http://localhost:8081/api/v1/benutzer").then((response) => {
                response.json().then((data) => {
                    this.allBenutzer = data;
                    console.log(data);
                });
            });
        },
        login(e) {
            e.preventDefault();
            for(let x in this.allBenutzer){
                if(x.ben)
            }
        }
    }
}
</script>
<template>

    <div v-for="benutzer in allBenutzer" :id="benutzer.id">
        <p>Benutzername</p><span>{{ benutzer.benutzername }}</span>
        <p>E-Mail</p><span>{{ benutzer.email }}</span>
    </div>
    <div>
        <form>
            <label for="benutzername"><b>Benutzername</b></label>
            <input v-model="this.benutzername" type="text" placeholder="Enter Username" name="benutzername" required>

            <label for="kennwort"><b>Benutzername</b></label>
            <input v-model="this.password" type="password" placeholder="Enter Password" name="kennwort" required>

            <button @click="login($event)" id="login">Einloggen</button>
        </form>
    </div>

</template>
