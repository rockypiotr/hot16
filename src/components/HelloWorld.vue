<template>
  <v-container>
    <v-timeline>
      <v-timeline-item v-for="item in ytData.data.items" v-bind:key="item.id.videoId" hide-dot>
        <span slot="opposite">{{ item.snippet.publishTime }}</span>
        <v-lazy
          v-model="isActive"
          :options="{
            threshold: 0.5,
          }"
          min-height="500"
          transition="fade-transition"
        >
          <v-card dark hover class="elevation-2">
            <v-card-title class="title headline">Tytuł: {{ item.snippet.title }}</v-card-title>
            <v-card-text class="text--primary pa-0">
              <youtube class="center" :video-id="item.id.videoId" ref="youtube" fitParent />
              <blockquote class="blockquote">{{ item.snippet.description }}</blockquote>
            </v-card-text>
          </v-card>
        </v-lazy>
      </v-timeline-item>
    </v-timeline>
  </v-container>
</template>

<style lang="sass">
@import url('https://fonts.googleapis.com/css?family=Roboto+Condensed')

li
  list-style-type: none

html, body
  font-family: 'Roboto Condensed', sans-serif

#app
  font-family: 'Roboto Condensed', sans-serif
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
      hideDot: false,
    };
  },

  mounted() {
    axios
      .get(
        'https://www.googleapis.com/youtube/v3/search?part=snippet&maxResults=6&order=date&q=%23hot16challenge2&type=video&videoDefinition=high&key=AIzaSyCYdyp8ar2W8gOpDrIW1cRfeeVMqMcASH4',
      )
      .then((response) => {
        this.ytData = response;
      });
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
