<script>
export default {
    data() {
        return {
            email: "",
            kennwort: ""
        }
    },
    created() {
    },
    methods: {
        async login(e) {
            e.preventDefault();
            console.log("E-Mail: " + this.email);
            console.log("Kennwort: " + this.kennwort);
            let body = {
                "email": this.email,
                "password": this.kennwort
            }
            await fetch("http://localhost:8081/api/v1/benutzer/check-login", {
                method: 'POST',
                body: body,
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                },
            }).then((res) => {
                res.json().then((data) => {
                    console.log(data);
                })
            })
        },
        onInput() {
            console.log("E-Mail: " + this.email);
            console.log("Kennwort: " + this.kennwort);
        }
    }
}
</script>
<template>
    <form class="row">
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
                <button @click="login($event)" class="btn btn-primary">Login</button>
            </div>
        </div>
    </form>
</template>
