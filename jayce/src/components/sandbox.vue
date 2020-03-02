<template>
  <v-app id="sandbox">
    <v-navigation-drawer
      v-model="primaryDrawer.model"
      :clipped="primaryDrawer.clipped"
      :floating="primaryDrawer.floating"
      :mini-variant="primaryDrawer.mini"
      :permanent="primaryDrawer.type === 'permanent'"
      :temporary="primaryDrawer.type === 'temporary'"
      disable-resize-watcher="true"
      app
      overflow>
      <!-- <h1 class="title font-weight-thin text-center text--primary">Jayce Vogt</h1>
      <hr style="opacity: 0.1;"/> -->
      <v-list>
      <v-list-item-group v-model="model">
        <v-list-item
          v-for="(post,index) in posts" :key="post.slug + '_' + index"
        >
          <v-list-item-content>
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
      app
    >
      <v-app-bar-nav-icon
        v-if="primaryDrawer.type !== 'permanent'"
        @click.stop="primaryDrawer.model = !primaryDrawer.model"
      />
      <v-toolbar-title>Jayce Vogt</v-toolbar-title>
    </v-app-bar>

    <v-content>
      <v-container fluid>
        <v-list>
            <v-card>
                <v-card-title>Test Post</v-card-title>
                <v-card-subtitle>10/16/19</v-card-subtitle>
                <v-card-text>Wowwwwwwwwwwwwwwwwwwwwwwwwwwwww</v-card-text>
                <v-card-actions>
                    <v-btn>Download .STL Files</v-btn>
                </v-card-actions>
            </v-card>
        </v-list>
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
    import { butter } from '@/buttercms'
  export default {
    name: 'sandbox',
    data: () => ({
        posts: {},
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
        items: [
        {
          text: 'A Cool Gun',
          date: '10/12/19'
        },
        {
          text: 'Printing Gone Wrong',
          date: '10/12/19'
        },
        {
          text: 'Wow weird',
          date: '10/12/19'
        },
        {
          text: 'Amazing',
          date: '10/12/19'
        },
      ],
      model: 1,
    }),
    methods: {
      getPosts() {
        butter.post.list({
          page: 1,
          page_size: 100
            }).then((res) => {
          console.log(res.data)
          this.posts = res.data.data
        })
      }
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