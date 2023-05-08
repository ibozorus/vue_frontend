<script>
export default {
    data() {
        return {
            benutzername: "",
            email: "",
            kennwort: "",
            meldung: ""
        }
    },
    created() {
    },
    methods: {
        async register(e) {
            e.preventDefault();
            console.log("E-Mail: " + this.email);
            console.log("Kennwort: " + this.kennwort);
            let body = {
                "benutzername": this.benutzername,
                "email": this.email,
                "password": this.kennwort
            }
            await fetch("http://localhost:8081/api/v1/benutzer", {
                method: 'POST',
                body: JSON.stringify(body),
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                },
            }).then((res) => {
                res.json().then((data) => {
                    console.log(data);
                    this.setMeldung(data);
                })
            })
        },
        onInput() {
            console.log("Benutzername: " + this.benutzername);
            console.log("E-Mail: " + this.email);
            console.log("Kennwort: " + this.kennwort);
        },
        setMeldung(isSuccess) {
            if (isSuccess === true) {
                this.meldung = "Erfolgreich!"
            } else {
                this.meldung = "Fehlgeschlagen!"
            }
        },
        changeToLoginPage(){

            this.$emit('clicked', 'login')
        }
    }
}
</script>
<template>
    <form class="row">
        <div class="row col-12 align-self-center">
            <div class="col-2 align-self-center offset-5">
                <label for="benutzername">Benutzername</label>
                <input @input="onInput" v-model="this.benutzername" type="text" name="benutzername" required>
            </div>
        </div>
        <div class="row col-12 align-self-center">
            <div class="col-2 align-self-center offset-5">
                <label for="email">E-Mail</label>
                <input @input="onInput" v-model="this.email" type="email" name="email" required>
            </div>
        </div>
        <div class="row col-12 align-self-center">
            <div class="col-2 align-self-center offset-5">
                <label for="kennwort">Kennwort</label>
                <input @input="onInput" v-model="this.kennwort" type="password" name="kennwort" required>
            </div>
        </div>
        <div class="row col-12 align-self-center">
            <div class="col-2 align-self-center offset-5">
                <button @click="register($event)" class="btn btn-primary">Register</button>
            </div>
        </div>
        <div class="row col-12 align-self-center">
            <div class="col-2 align-self-center offset-5">
                <label for="meldung">Meldung</label>
                <input v-model="this.meldung" type="text" name="meldung" readonly>
            </div>
        </div>

        <div class="row col-12 align-self-center">
            <div class="col-2 align-self-center offset-5">
                <button @click="changeToLoginPage()" class="btn btn-primary">Zurück zum Login</button>
            </div>
        </div>
    </form>
    <div class="row col-12 align-self-center">
    </div>
</template>
