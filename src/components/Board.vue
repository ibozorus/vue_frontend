<script>
import Eintrag from "@/components/Eintrag.vue";

export default {
    props: {
        "boardId": Number,
        "boardText": String
    },
    components: {Eintrag},
    data() {
        return {
            "eintraege": [],
            "anzahlEintraege": 0

        }
    },
    created() {
        this.getEintraege();
    },
    mounted() {
    },
    methods: {
        async getEintraege() {
            return await fetch("http://localhost:8081/api/v1/eintrag/" + this.boardId, {
                method: 'GET',
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                },
            }).then((res) => {
                res.json().then((data) => {
                    console.log(data);
                    this.anzahlEintraege = data.length;
                    this.eintraege = data;
                    console.log(this.eintraege[0].board.id)


                })
            })
        }
    }
}
</script>
<template>
    <table :id="'board-'+this.boardId">
        <tr>
            <th>{{ boardText }}</th>
        </tr>

        <Eintrag v-if="anzahlEintraege > 0" v-for="eintrag in eintraege" :eintrag-id="eintrag.id"
                 :eintrag-text="eintrag.text">

        </Eintrag>

    </table>
</template>
<style>
</style>
