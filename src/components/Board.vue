<script>
import {isProxy, toRaw} from 'vue';

export default {

    components: {},
    data() {
        return {
            "eintraege": [],
            "anzahlEintraege": 0,
            "boards": [],
            "anzahlBoards": 0
        }
    },
    created() {
        this.getBoards().then(() => {
            this.getEintraege();
        });
    },
    methods: {
        async getEintraege() {
            return await fetch("http://localhost:8081/api/v1/eintrag/1", {
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
                    console.log(this.eintraege[0].board_id)


                })
            })
        }
        ,
        async getBoards() {
            return await fetch("http://localhost:8081/api/v1/board/1", {
                method: 'GET',
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                },
            }).then((res) => {
                res.json().then((data) => {
                    console.log(data);
                    this.anzahlBoards = data.length;
                    this.boards = data;

                })
            })
        }
    }
}
</script>
<template>

    <div v-if="anzahlBoards > 0" v-for="board in boards" class="col-4">
        <table :id="'board-'+board.id">
            <tr>
                <th>{{ board.text }}</th>
            </tr>
            <div v-for="eintrag in eintraege">
                <tr v-if="eintrag.board.id === board.id" :id="'eintrag-'+eintrag.id" >
                    <td>{{ eintrag.text }}</td>
                </tr>
            </div>
        </table>
    </div>
</template>
<style>
</style>
