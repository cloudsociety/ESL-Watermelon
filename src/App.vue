<template>
  <div class="container">
    <figure class="image" @click="getRandomImage">
      <img :src="randomImage.src" alt="" class="image__face" :style="{backgroundColor:color.cssName}">
      <figcaption class="image__text">A <em>{{color.displayName}}</em> {{randomImage.name | fixName}}</figcaption>
    </figure>
  </div>
</template>

<script>
import _ from 'lodash'
import {ImagesMixin} from './ImagesMixin.js';

export default {
  data () {
    return {
      // msg: 'Welcome to Your Vue.js App'
      randomImage: {},
      color: {}
    }
  },
  methods: {
    getRandomImage(){
      let selectedImage = _.shuffle(Object.keys(this.images)).slice(0,1)[0];
      this.randomImage = { name: selectedImage, src: this.images[selectedImage] };

      // Let's colour this up
      let colors = [
        {cssName:"hotpink",displayName:"Pink"},
        {cssName:"red",displayName:"Red"},
        {cssName:"orange",displayName:"Orange"},
        {cssName:"yellow",displayName:"Yellow"},
        {cssName:"limegreen",displayName:"Green"},
        {cssName:"dodgerblue",displayName:"Blue"},
        {cssName:"purple",displayName:"Purple"},
        {cssName:"saddlebrown",displayName:"Brown"}
      ];
      let selectRandom = Math.floor(Math.random() * colors.length);
      this.color = colors.slice(selectRandom,selectRandom+1)[0];
    }
  },
  mixins: [ImagesMixin],
  filters: {
    fixName: (value) => {
      return value.split(".")[0].replace('-', ' ');
    }
  },
  created(){
    this.getRandomImage();
  }
}
</script>

<style lang="scss">
body {
  background-color: #ddd;
  font: 1em Arial,sans-serif;
}

.container {
  position: absolute;
  top: 0;left: 0;bottom: 0;right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

.image {
  width: 600px; height: 600px;
  border-radius: 10px;
  box-shadow: 0 0 5px #999;
  margin: 0;padding: 0;
  position: relative;
  overflow: hidden;

  &__face {
    margin: 0;padding: 0;
    width: 600px; height: 600px;
    object-fit:cover;
  }

  &__text {
    position: absolute;
    left: 0;bottom: 0;right: 0;
    background-color: rgba(0,0,0,.5);
    color: #fff;
    font-size: 3em;
    text-align: center;
    text-transform: capitalize;
    padding: 10px;
  }
}
</style>
