<script>
import Eintrag from "@/components/Eintrag.vue";

export default {
    props: {
        "boardId": Number,
        "boardText": String,
        "apiUrl": String
    },
    components: {Eintrag},
    data() {
        return {
            "eintraege": [],
            "anzahlEintraege": 0,
            "newEintragtext": null

        }
    },
    created() {
        this.getEintraege();
    },
    mounted() {
    },
    methods: {
        async getEintraege() {
            return await fetch(this.apiUrl + "api/v1/eintrag/" + this.boardId, {
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
                "text": this.newEintragtext,
                "board": {
                    "id": boardId,
                    "benutzer": {
                        "id": sessionStorage.getItem("benutzerId")
                    }
                }
            }
            await fetch(this.apiUrl + "api/v1/eintrag", {
                method: "POST",
                body: JSON.stringify(body),
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                }
            }).then(() => {
                this.getEintraege();
                this.newEintragtext = "";
            });
        }
    }
}
</script>
<template>
    <div class="col-4">
        <table class="table table-bordered  table-hover table-striped table-sm" :id="'board-'+this.boardId">
            <thead>
            <tr>
                <th>{{ boardText }}
                </th>
            </tr>
            </thead>
            <tbody>
            <Eintrag @reload-eintraege="getEintraege" v-if="anzahlEintraege > 0" v-for="eintrag in eintraege"
                     :eintrag-id="eintrag.id"
                     :eintrag-text="eintrag.text"
                     :api-url="apiUrl">

            </Eintrag>
            <tr>

                <td>
                    <div class="container">
                        <div class="row">
                            <input class="eintragInput col-10" v-model="this.newEintragtext" type="text"
                                   placeholder="Add new Eintrag"
                                   required>
                            <button @click="addEintrag(this.boardId)" type="button" class="btn col-2 align-self-end"><i
                                    class="fa-solid fa-floppy-disk"></i>
                            </button>
                        </div>
                    </div>
                </td>
            </tr>
            </tbody>

        </table>


    </div>
</template>
<style>
.eintragInput {
    border: 0px;
    background: transparent;
}

.eintragInput:focus {
    border: 0px;
    background: transparent;
    outline: none;
}
</style>
