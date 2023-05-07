<script>

export default {
    props: {
        "eintragId": Number,
        "eintragText": String
    },
    components:{} ,
    data() {
        return {

        }
    },
    created() {
    },
    mounted() {
    },
    methods: {

    }
}
</script>
<template>
        <tr :id="'Eintrag-' + eintragId">
            <td>{{ eintragText }}</td>
        </tr>
</template>
<style>
</style>
