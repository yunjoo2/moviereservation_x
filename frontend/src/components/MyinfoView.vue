<template>

    <v-data-table
        :headers="headers"
        :items="myinfo"
        :items-per-page="5"
        class="elevation-1"
    ></v-data-table>

</template>

<script>
    const axios = require('axios').default;

    export default {
        name: 'MyinfoView',
        props: {
            value: Object,
            editMode: Boolean,
            isNew: Boolean
        },
        data: () => ({
            headers: [
                { text: "id", value: "id" },
            ],
            myinfo : [],
        }),
          async created() {
            var temp = await axios.get(axios.fixUrl('/myinfos'))

            temp.data._embedded.myinfos.map(obj => obj.id=obj._links.self.href.split("/")[obj._links.self.href.split("/").length - 1])

            this.myinfo = temp.data._embedded.myinfos;
        },
        methods: {
        }
    }
</script>

