<template v-if="inputPost">
    <v-card>
        <v-card-title>{{inputPost.title}}<h5 v-bind:class="inputPost.categories[0].slug + ' category'">{{inputPost.categories[0].name}}</h5></v-card-title>
        <v-card-subtitle>{{new Date(inputPost.created).toDateString()}}</v-card-subtitle>
        <v-card-text><div v-html="inputPost.body"></div></v-card-text>
        <v-card-actions v-if="inputPost.tags.length">
            <div class="button" v-for="(button,index) in inputPost.tags" :key="index"><v-btn v-bind:href="button.name">{{button.slug}}</v-btn></div>
        </v-card-actions>
    </v-card>
</template>

<script>
  export default {
    name: 'project',
    props: {
        inputPost: Object,
    }
  }
</script>

<style scoped>
    .button {
        margin-right: 8px;
    }

    .category {
        margin: 8px 0px 8px 5px;
        font-size: 0.55em;
        font-weight: 400;
        line-height: 1.3;
        padding: 4px;
        opacity: 0.9;
        text-transform: uppercase;
        border-radius: 10px;
        cursor: default;
        box-shadow: rgba(51, 51, 51, 0.2) 0px 3px 4px 0px;
    }
</style>