<template>
  <v-app>

    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <v-container>

        <h1 class="mb-3">Text Tags Component</h1>

        <v-row class="justify-space-between">

          <v-col class="d-flex col-12">
            <text-tags :tags="tags" alignment="left" />
          </v-col>
    
          <v-col class="d-flex col-12">
            <text-tags :tags="tags" alignment="justify" />
          </v-col>

        </v-row>
      
      
        <v-row>

          <v-col class="d-flex col-6">
            <text-tags :tags="tags" alignment="left" />
          </v-col>

          <v-col class="d-flex col-6">
            <text-tags :tags="tags" alignment="justify" />
          </v-col>

        </v-row>

    </v-container>
    </v-main>
  </v-app>
</template>

<script>
import TextTags from '@/components/TextTags';

export default {
  name: 'App',

  components: {
    TextTags,
  },

  data: () => ({
    tags: [
      {
        text: 'text1 lorem',
      },
      {
        text: 'text1 lorem',
        icon: 'mdi-alpha-a-circle'
      },
      {
        text: 'text1 lorem',
        icon: 'mdi-alpha-b-circle'
      },
      {
        text: 'text4 lorem ipsum',
        icon: 'mdi-alpha-c-circle'
      },
      {
        text: 'text1 lorem',
      },
      // {
      //   text: 'text6',
      //   icon: 'mdi-alpha--circle'
      // },
      // {
      //   text: 'text7',
      //   icon: 'icon-name-7'
      // },
      // {
      //   text: 'text8',
      //   icon: 'icon-name-8'
      // },    
    ]
  }),
};
</script>
