<template>
  <div id="app">
    <img src="./assets/logo.png">
    <button @click="initialize()">Initialize</button>
    <button @click="record()">Record</button>
    <button @click="stop()">Stop</button>
    <button @click="play()">Play</button>
    <button @click="release()">Release</button>
    <pre>{{ mediaRec }}</pre>
    <pre>{{ mediaRec.mediaStatus }}</pre>
  </div>
</template>

<script>
import Vue from 'vue';

/* eslint-disable no-alert */
export default {
  data() {
    return {
      // cordova: Vue.cordova,
      mediaRec: '',
    };
  },
  methods: {
    initialize() {
      const currentdate = new Date();
      const datetime = currentdate.getFullYear().toString()
        + (currentdate.getMonth() + 1).toString()
        + currentdate.getDate().toString()
        + currentdate.getHours().toString()
        + currentdate.getMinutes().toString()
        + currentdate.getSeconds().toString();
      this.mediaRec = new Vue.cordova.Media(`hello${datetime}.mp3`,
        // success callback
        () => {
          window.alert('recordAudio():Audio Success');
        },

        // error callback
        (err) => {
          window.alert(`recordAudio():Audio Error: ${err.message}`);
        }, (status) => {
          alert(status);
        },
      );
    },
    record() {
      this.mediaRec.startRecord();
    },
    stop() {
      this.mediaRec.stopRecord();
    },
    play() {
      this.mediaRec.play();
    },
    release() {
      this.mediaRec.release();
    },
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
