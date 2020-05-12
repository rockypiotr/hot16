<template>
  <v-container>
    <ul id="example">
      <li v-for="item in ytData.data.items" v-bind:key="item.id.videoId">
        <h1>Tytuł: {{ item.snippet.title }}</h1>
        <youtube :video-id="item.id.videoId" ref="youtube"/>
        <p>Opis:</p>
        <p>{{ item.snippet.description }}</p>
      </li>
    </ul>
  </v-container>
</template>

<style lang="sass" scoped>
  li
    list-style-type: none
</style>

<script>
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';

Vue.use(axios, VueAxios);

export default {
  name: 'HelloWorld',

  data() {
    return {
      ytData: null,
    };
  },

  mounted() {
    axios
      .get('https://www.googleapis.com/youtube/v3/search?part=snippet&maxResults=20&order=date&q=%23hot16challenge2&type=video&videoDefinition=high&key=AIzaSyCuBffhWIOOZlOg19GdJyz9x8YgCq-f2kE')
      .then((response) => { this.ytData = response; });
  },

  computed: {
    player() {
      return this.$refs.youtube.player;
    },
  },

  methods: {
    playVideo() {
      this.player.playVideo();
    },
    playing() {
      console.log('We are watching!!!');
    },
  },
};
</script>
