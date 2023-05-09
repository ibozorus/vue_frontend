<script>

export default {
    props: {
        "eintragId": Number,
        "eintragText": String
    },
    components: {},
    data() {
        return {}
    },
    created() {
    },
    mounted() {
    },
    methods: {
        async deleteEintrag(eintragId) {
            await fetch("http://localhost:8081/api/v1/eintrag/" + eintragId, {
                method: "DELETE",
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                }
            }).then(() => {
                this.reloadEintraege();
            });
        },
        reloadEintraege() {
            this.$emit('reload-eintraege', 'boards')
        }
    }
}
</script>
<template>
    <tr :id="'Eintrag-' + eintragId">
        <td>

            <div class="container">
                <div class="row">
                    <input class="eintragInput col-10" type="text" :value="this.eintragText" readonly>
                    <button @click="deleteEintrag(eintragId)" type="button" class="btn align-self-end col-2"><i
                            class="fa-solid fa-minus"></i></button>
                </div>
            </div>
        </td>
    </tr>
</template>
<style>
</style>
