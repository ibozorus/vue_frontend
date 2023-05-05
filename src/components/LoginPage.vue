<script>
export default {
    data() {
        return {
            email: "",
            kennwort: "",
            meldung: ""
        }
    },
    created() {
    },
    methods: {
        changeToBoard() {
            this.$emit('clicked', 'boards')
        }
        ,
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
                body: JSON.stringify(body),
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                },
            }).then((res) => {
                res.json().then((data) => {
                    console.log(data);
                    this.setMeldung(data);
                    if(data === true) {
                        this.changeToBoard();
                    }
                })
            })
        },
        onInput() {
            console.log("E-Mail: " + this.email);
            console.log("Kennwort: " + this.kennwort);
        },
        setMeldung(isSuccess) {
            // if (isSuccess === true) {
            //     this.meldung = "Erfolgreich!";
            //     alert("Erfolgreich!");
            // } else {
            //     this.meldung = "Fehlgeschlagen!";
            //     alert("Fehlgeschlagen!");
            // }
        }
    }
}
</script>
<template>
    <form class="row">
        <div class="row col-12 align-self-center">
            <div class="row col-2 align-self-center offset-5">
                <label class="col-12" for="email">E-Mail</label>
                <input class="col-12" @input="onInput" v-model="this.email" type="email" name="email" required>
            </div>
        </div>
        <div class="row col-12 align-self-center">
            <div class="col-2 align-self-center offset-5">
                <label class="col-12" for="kennwort">Kennwort</label>
                <input class="col-12" @input="onInput" v-model="this.kennwort" type="password" name="kennwort" required>
            </div>
        </div>
        <div class="row col-12 align-self-center">
            <div class="col-2 align-self-center offset-5">
                <button @click="login($event)" class="btn btn-primary">Login</button>
            </div>
        </div>
        <!--        <div class="row col-12 align-self-center">-->
        <!--            <div class="row col-2 align-self-center offset-5">-->
        <!--                <label class="col-12" for="meldung">Meldung</label>-->
        <!--                <input class="col-12" v-model="this.meldung"  type="text" name="meldung" >-->
        <!--            </div>-->
        <!--        </div>-->
    </form>
    <div class="row col-12 align-self-center">
    </div>
</template>
