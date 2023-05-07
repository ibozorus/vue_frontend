<script>
import {isProxy, toRaw} from 'vue';

export default {
    props: {
        "boardId": Number,
        "boardText": String
    },
    components: {},
    data() {
        return {

        }
    },
    created() {
        // this.getBoards().then(() => {
        //     this.getEintraege();
        // });
        // console.log(board);
    },
    mounted() {
        console.log(this.boardId)
        console.log(this.boardText)
    },
    methods: {
        // async getEintraege() {
        //     return await fetch("http://localhost:8081/api/v1/eintrag/1", {
        //         method: 'GET',
        //         headers: {
        //             'Accept': 'application/json',
        //             'Content-Type': 'application/json'
        //         },
        //     }).then((res) => {
        //         res.json().then((data) => {
        //             console.log(data);
        //             this.anzahlEintraege = data.length;
        //             this.eintraege = data;
        //             console.log(this.eintraege[0].board_id)
        //
        //
        //         })
        //     })
        // }
        // ,
        // async getBoards() {
        //     return await fetch("http://localhost:8081/api/v1/board/1", {
        //         method: 'GET',
        //         headers: {
        //             'Accept': 'application/json',
        //             'Content-Type': 'application/json'
        //         },
        //     }).then((res) => {
        //         res.json().then((data) => {
        //             console.log(data);
        //             this.anzahlBoards = data.length;
        //             this.boards = data;
        //
        //         })
        //     })
        // }
    }
}
</script>
<template>


    <table :id="'board-'+this.boardId">
        <tr>
            <th>{{ boardText }}</th>
        </tr>
        <!--            <div v-for="eintrag in eintraege">-->
        <!--                <tr v-if="eintrag.board.id === board.id" :id="'eintrag-'+eintrag.id" >-->
        <!--                    <td>{{ eintrag.text }}</td>-->
        <!--                </tr>-->
        <!--            </div>-->
    </table>
</template>
<style>
</style>
