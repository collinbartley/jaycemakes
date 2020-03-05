<template v-if="inputPost">
    <v-card>
        <v-card-title>{{inputPost.title}}</v-card-title>
        <v-card-subtitle>{{new Date(inputPost.created).toDateString()}}</v-card-subtitle>
        <v-card-text><div v-html="inputPost.body"></div></v-card-text>
        <v-card-actions v-if="buttons">
            <div class="button" v-for="(button,index) in buttons" :key="index"><v-btn v-bind:href="buttons[index][1]">{{buttons[index][0]}}</v-btn></div>
            <!-- <v-btn v-bind:href="buttons[1]">{{buttons[0]}}</v-btn> -->
        </v-card-actions>
    </v-card>
</template>

<script>
  export default {
    name: 'BlogPost',
    props: {
        inputPost: Object,
        buttons: null
    }
  }
</script>

<style scoped>
    .button {
        margin-right: 8px;
    }
</style>