<script>
import Board from "@/components/Board.vue";

export default {

    components: {
        "Board": Board
    },
    data() {
        return {
            "boards": [],
            "anzahlBoards": 0
        }
    },
    created() {
        this.getBoards();
    },
    methods: {
        async getBoards() {
            let benutzerId = sessionStorage.getItem("benutzerId");
            return await fetch("http://localhost:8081/api/v1/board/" + benutzerId, {
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
    <div>
        <Board v-if="anzahlBoards > 0" v-for="board in boards" :board-id="board.id" :board-text="board.text">

        </Board>
    </div>
</template>
<style>
</style>
