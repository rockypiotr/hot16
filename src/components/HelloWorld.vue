<template>
  <v-container>
    <youtube :video-id="ytData.data.items[2].id.videoId" ref="youtube"/>
    <p>{{ ytData.data.items[0].id.videoId }}</p>
    <p>{{ ytData.data.items[0].snippet.title }}</p>
    <p>{{ ytData.data.items[0].snippet.description }}</p>
  </v-container>
</template>

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
      videoId: 'lG0Ys-2d4MA',
    };
  },

  mounted() {
    axios
      .get('https://www.googleapis.com/youtube/v3/search?part=snippet&maxResults=20&order=date&q=%23hot16challenge&type=video&videoDefinition=high&key=AIzaSyCuBffhWIOOZlOg19GdJyz9x8YgCq-f2kE')
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
      console.log(' we are watching!!!');
    },
  },
};
</script>
