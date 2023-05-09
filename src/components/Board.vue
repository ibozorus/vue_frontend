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
                    console.log("Boardid: " + this.eintraege[0].board.id)


                })
            })
        },
        async addEintrag(boardId) {
            let body = {
                "text": "Eintrag 5",
                "board": {
                    "id": boardId,
                    "benutzer": {
                        "id": sessionStorage.getItem("benutzerId")
                    }
                }
            }

            await fetch("http://localhost:8081/api/v1/eintrag", {
                method: "POST",
                body: JSON.stringify(body),
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                }
            }).then(() => {
                this.getEintraege();
            });
        }
    }
}
</script>
<template>
    <div class="col-3">
        <table class="table table-bordered  table-hover table-striped table-sm" :id="'board-'+this.boardId">
            <thead>
            <tr>
                <th>{{ boardText }}
                    <button @click="addEintrag(this.boardId)" class="btn btn-primary">Add</button>
                </th>
            </tr>
            </thead>
            <tbody>
            <Eintrag @reload-eintraege="getEintraege" v-if="anzahlEintraege > 0" v-for="eintrag in eintraege"
                     :eintrag-id="eintrag.id"
                     :eintrag-text="eintrag.text">

            </Eintrag>
            </tbody>

        </table>

    </div>
</template>
<style>
</style>
