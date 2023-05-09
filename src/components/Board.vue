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
            "anzahlEintraege": 0,
            "newEintragtext": null,
            "selectedBoard": 0

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
        async addEintrag() {
            let body = {
                "text": this.newEintragtext,
                "board": {
                    "id": this.selectedBoard,
                    "benutzer": {
                        "id": sessionStorage.getItem("benutzerId")
                    }
                }
            }
            console.log("body:" + JSON.stringify(body))
            console.log(this.newEintragtext)
            console.log(this.selectedBoard)

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
        },
        openModal(modalId, boardId) {
            this.selectedBoard = boardId;
            console.log(this.selectedBoard)
            console.log(boardId)
            $('#' + modalId).modal('toggle');
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
                    <button @click="openModal('add-eintrag-modal', this.boardId)" class="btn btn-primary">Add</button>
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

        <!-- Modal -->
        <div class="modal fade" id="add-eintrag-modal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel"
             aria-hidden="true">
            <div class="modal-dialog" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                            <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <div class="modal-body">
                        <label for="neweintragtext">Eintrag Text</label>
                        <input v-model="this.newEintragtext" type="text" name="neweintragtext" required>

                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                        <button @click="addEintrag()" type="button" class="btn btn-primary">Save Eintrag</button>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>
<style>
</style>
