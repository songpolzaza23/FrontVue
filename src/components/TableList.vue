<template>
    <v-data-table
          :headers="headers"
          :items="desserts"
          class="elevation-2 ma-10 "
        ></v-data-table>
</template>

<script>
    export default {
        name: "TableList",
        props:["headers","desserts"]
    }
</script>