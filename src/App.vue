<template>
  <v-app id="inspire">
    <v-navigation-drawer
      v-model="drawer"
      app
      clipped
    >
      <v-list dense>
        <v-list-item link>
          <v-list-item-action>
            <v-icon>mdi-view-dashboard</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>News</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item link>
          <v-list-item-action>
            <v-icon>mdi-settings</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Settings(Not usable for now)</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      clipped-left
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title>Application</v-toolbar-title>
    </v-app-bar>

    <v-content>
      <v-container
        class="fill-height"
        fluid
      >
        <v-row
          align="center"
          justify="center"
        >
          <v-col class="shrink">
            <v-tooltip right>
              <template>
                <ol>
                  <li v-for="(item, index) in msst" :key="index">{{item}}</li>
                </ol>
                

              </template>
              <span>Codepen</span>
            </v-tooltip>
          </v-col>
        </v-row>
      </v-container>
    </v-content>

    <v-footer app>
      <span>&copy; 2019</span>
    </v-footer>
  </v-app>
</template>

<script>
//import HelloWorld from './components/HelloWorld';

  export default {
    props: {
      source: String,
    },
    data: () => ({
      drawer: null,
      msst:[]
    }),
    created () {
      this.$vuetify.theme.dark = true
    },
    methods:{
      updFacts(){
        this.axios.get("http://188.225.47.187/api/news/get_top_headlines.php").then((res)=>{
          this.msst=res.data['articles']

        })
      }
    },
    mounted(){
      this.updFacts();
    }
  }
</script>
