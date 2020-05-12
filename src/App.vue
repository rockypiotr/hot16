<template>
  <v-app>
    <v-app-bar
      app
      dark
      dense
      collapse
    >
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-app-toolbar-title>Hot16</v-app-toolbar-title>
    </v-app-bar>
  <HelloWorld/>
  </v-app>
</template>

<script>
import Vue from 'vue';
import VueYoutube from 'vue-youtube';
import HelloWorld from './components/HelloWorld.vue';

Vue.use(VueYoutube);

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script>
