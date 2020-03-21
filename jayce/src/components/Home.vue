<template>
  <v-app id="home">
    <v-navigation-drawer
      v-model="primaryDrawer.model"
      :clipped="primaryDrawer.clipped"
      :floating="primaryDrawer.floating"
      :mini-variant="primaryDrawer.mini"
      :permanent="primaryDrawer.type === 'permanent'"
      :temporary="primaryDrawer.type === 'temporary'"
      :disable-resize-watcher="true"
      app
      overflow>
      <!-- <h1 class="title font-weight-thin text-center text--primary">Jayce Vogt</h1>
      <hr style="opacity: 0.1;"/> -->
      <v-list :dense="true">
      <v-list-item-group v-model="model" :mandatory="true">
        <v-list-item
          v-for="(post,index) in posts" :key="post.slug + '_' + index"
        >
          <v-list-item-content @click="getPost(post.slug)">
            <v-list-item-title v-text="post.title"></v-list-item-title>
            <v-list-item-subtitle v-text="new Date(post.created).toDateString()"></v-list-item-subtitle>
            <span v-bind:class="'category ' + post.categories[0].slug"></span>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
    </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="primaryDrawer.clipped"
      :dense="true"
      :flat="true"
      app
    >
      <v-app-bar-nav-icon
        v-if="primaryDrawer.type !== 'permanent'"
        @click.stop="primaryDrawer.model = !primaryDrawer.model"
      />
      <v-toolbar-title>Jayce Vogt</v-toolbar-title>
    </v-app-bar>

    <v-content v-if="selectedPost">
      <v-container fluid>
        <project v-bind:inputPost="this.selectedPost"></project>
      </v-container>
    </v-content>

    <v-footer
      :inset="footer.inset"
      app
    >
      <div>
        <span style="opacity: 0.5;" class="px-4">&copy; {{ new Date().getFullYear() }} made by collin bartley - <a href="https://cobar.co" class="orange--text">cobar.co</a></span>
        <div><a href="https://buttercms.com"><img style="width: 130px;" src="https://cdn.buttercms.com/RyJ7UhcVTCRqrCFXwgCo" alt="ButterCMS"></a></div>
      </div>
    </v-footer>
  </v-app>
</template>

<script>
    import project from "./Project.vue";
    import { butter } from '@/buttercms'
  export default {
    name: 'home',
    components: {
        project,
    },
    data: () => ({
        posts: {},
        selectedPost: null,
        drawers: ['Default (no property)', 'Permanent', 'Temporary'],
        primaryDrawer: {
            model: null,
            type: 'default (no property)',
            clipped: true,
            floating: false,
            mini: false,
        },
        footer: {
            inset: false,
        },
      model: 1,
    }),
    methods: {
      getPosts() {
        butter.post.list({
          page: 1,
          page_size: 100
            }).then((res) => {
          this.posts = res.data.data
          this.posts.forEach(post => {
            if(post.tags.length) {
              post.tags.forEach(tag => {
                tag.slug = tag.slug.replace("-", " ");
              })
            }
          });
          this.selectedPost = this.posts[0];
        })
      },
      getPost(slug) {
        this.posts.filter(_post => {
            if(_post.slug == slug) {
                this.selectedPost = _post;
            }
          });
        },
    },
    created() {
      this.getPosts()
    }
  }
</script>

<style lang="scss" scoped>
  .category {
    width: 7px;
    height: 100%;
    position: absolute;
    right: 0;
    opacity: 0.5;
  }

  .image {
    position: relative;
    right: 0;
    margin: 5px;
    float: right;
  }
</style>

<style lang="scss">
  .red {
    background-color: red;
  }

  .orange {
    background-color: orange;
  }

  .yellow {
    background-color: yellow;
  }

  .green {
    background-color: green;
  }

  .blue {
    background-color: blue;
  }

  .indigo {
    background-color: indigo;
  }

  .violet {
    background-color: violet;
  }
</style>