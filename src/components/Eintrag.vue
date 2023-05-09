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
        <td>{{ eintragText }}
            <button @click="deleteEintrag(eintragId)" class="btn btn-primary">Delete</button>
        </td>
    </tr>
</template>
<style>
</style>
