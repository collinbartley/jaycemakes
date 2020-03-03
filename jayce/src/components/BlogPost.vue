<template v-if="inputPost">
    <v-card>
        <v-card-title>{{inputPost.title}}</v-card-title>
        <v-card-subtitle>{{new Date(inputPost.created).toDateString()}}</v-card-subtitle>
        <v-card-text><div v-html="inputPost.body"></div></v-card-text>
        <v-card-actions>
            <v-btn v-html="inputPost.summary"></v-btn>
        </v-card-actions>
    </v-card>
</template>

<script>
  export default {
    name: 'BlogPost',
    props: {
        inputPost: Object
    }
  }
</script>

<style scoped>
    .btn {
        border: solid black 2px;
        background: black;
        border-radius: 8px;
        padding: 5px;
        text-decoration: none;
        color: grey;
    }

    .btn:hover {
        border-radius: 0px;
    }
</style>