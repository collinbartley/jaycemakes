<template>
  <v-app id="sandbox">
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
      <v-list>
      <v-list-item-group v-model="model">
        <v-list-item
          v-for="(post,index) in posts" :key="post.slug + '_' + index"
        >
          <v-list-item-content @click="getPost(post.slug)">
            <v-list-item-title v-text="post.title"></v-list-item-title>
            <v-list-item-subtitle v-text="new Date(post.created).toDateString()"></v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
    </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="primaryDrawer.clipped"
      :dense="true"
      :flat="true"
      src="https://images.unsplash.com/photo-1506318137071-a8e063b4bec0?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1970&q=80"
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
        <BlogPost v-bind:inputPost="this.selectedPost"></BlogPost>
      </v-container>
    </v-content>

    <v-footer
      :inset="footer.inset"
      app
    >
      <span style="opacity: 0.5;" class="px-4">&copy; {{ new Date().getFullYear() }} made by collin bartley - <a href="https://cobar.co" class="orange--text">cobar.co</a></span>
    </v-footer>
  </v-app>
</template>

<script>
    import BlogPost from "./BlogPost.vue";
    import { butter } from '@/buttercms'
  export default {
    name: 'sandbox',
    components: {
        BlogPost,
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
          this.selectedPost = this.posts[0];
          console.log(this.posts);
        })
      },
      getPost(slug) {
        this.posts.filter(_post => {
            if(_post.slug == slug) {
                this.selectedPost = _post;
                console.log(this.selectedPost);
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
 .floating-button {
     position: absolute;
    z-index: 1000;
    left: 0;
    top: 0;
 }
</style>