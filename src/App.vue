<script>

import Login from './components/LoginPage.vue'
import Register from './components/RegisterPage.vue'
import BoardsUebersicht from "@/components/BoardsUebersicht.vue";
import config from './config/config.json'

export default {

    components: {
        "login": Login,
        "register": Register,
        "boards": BoardsUebersicht
    },
    data() {
        return {
            activeComp: 'login',
            benutzername: null,
            newBoardName: "",
            config: config
        }
    },
    created() {
        sessionStorage.clear();
    },
    methods: {
        getApiUrl() {
            let url = this.config.server.host + this.config.server.port
            return url;
        }
        ,
        onClickChild(value) {
            this.activeComp = value;
        },
        setBenutzername(benutzername) {
            this.benutzername = benutzername;
            console.log(this.benutzername);
        },
        showAbmelden() {
            if (this.activeComp === "login" || this.activeComp === "register") {
                return false;
            } else {
                return true;
            }
        },
        abmelden() {
            sessionStorage.removeItem("benutzerId");
            this.onClickChild("login");
            this.benutzername = null;

        },
        openModal(modalId) {
            $('#' + modalId).modal('toggle');
        }
        ,
        async createNewBoard() {
            let body = {
                "text": this.newBoardName,
                "benutzer": {
                    "id": sessionStorage.getItem("benutzerId")
                }
            }
            await fetch(this.getApiUrl() + "api/v1/board", {
                method: "POST",
                body: JSON.stringify(body),
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                }

            }).then((response) => {
                response.json().then((data) => {
                    console.log(data);
                }).then(() => {
                    this.openModal("add-board-modal")
                    this.$refs.childComp.getBoards();

                })
            })
        }
    }
}
</script>
<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">


        <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
                <a class="nav-link" v-if="benutzername != null">{{ this.benutzername }} <span
                        class="sr-only"></span></a>
            </li>
            <li class="nav-item active">
                <a class="nav-link" v-show="showAbmelden()" @click="abmelden()">
                    <i class="fa-solid fa-arrow-right-from-bracket"></i> <span
                        class="sr-only"></span></a>
            </li>
            <li class="nav-item active">
                <a class="nav-link" v-show="this.activeComp === 'boards'" @click="openModal('add-board-modal')"><i
                        class="fa-solid fa-plus"></i><span
                        class="sr-only"></span></a>
            </li>

        </ul>
    </nav>
    <div>
        <component ref="childComp" :api-url="getApiUrl()" @set-benutzername="setBenutzername" @clicked="onClickChild"
                   :is="activeComp"></component>
    </div>

  <!-- Modal -->
    <div class="modal fade" id="add-board-modal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel"
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
                    <label for="newboardname">Board Name</label>
                    <input v-model="this.newBoardName" type="text" name="newboardname" required>

                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                    <button @click="createNewBoard()" type="button" class="btn btn-primary">Save Board</button>
                </div>
            </div>
        </div>
    </div>
</template>
<style>
a:hover {
    cursor: pointer;
}
</style>
