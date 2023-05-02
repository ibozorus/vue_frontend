<script>
export default {
    data() {
        return {
            allBenutzer: []
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
        }
    }
}
</script>
<template>

            <div v-for="benutzer in allBenutzer" :id="benutzer.id">
                <p>Benutzername</p><span>{{benutzer.benutzername}}</span>
                <p>E-Mail</p><span>{{benutzer.email}}</span>
            </div>


</template>
