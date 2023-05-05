<script>


export default {

    components: {},
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
            await fetch("http://localhost:8081/api/v1/board/1", {
                method: 'GET',
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                },
            }).then((res) => {
                res.json().then((data) => {
                    console.log(data);
                    this.boards = data;
                    this.anzahlBoards = data.length;
                })
            })
        }
    }
}
</script>
<template>

    <div v-if="anzahlBoards > 0" v-for="board in boards" class="col-4">
        <table :id="'board-'+board.text">
            <tr>
                <th>{{ board.text }}</th>
            </tr>
            <tr>
                <td>Alfreds Futterkiste</td>
            </tr>
            <tr>
                <td>Centro comercial Moctezuma</td>
            </tr>
        </table>
    </div>
</template>
<style>
</style>
