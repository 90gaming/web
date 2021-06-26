<template>
  <hooper :autoPlay="true" :playSpeed="2000" style="max-width: 400px;;margin: auto;">
    <slide v-for="thumb in images" :key="thumb.id" class="bg-contain bg-center bg-no-repeat" v-bind:style="{ backgroundImage: 'url(' + url+thumb.formats.medium.url + ')' }" style="background-size: 100% 100%;">
    </slide>

    <hooper-navigation slot="hooper-addons"></hooper-navigation>
  </hooper>
</template>

<script>
import 'hooper/dist/hooper.css'
import {
  Hooper,
  Slide,
  Navigation as HooperNavigation
  } from 'hooper';

export default {
  props: ['images'],
  components: {
    Hooper,
    Slide,
    HooperNavigation
  },
  data(){
    return{
      url: process.env.baseURL
    }
  },
  mounted(){
    console.log('Thumbnail',this.images)
  }
}
</script>
<style>
.hooper-next,
.hooper-prev {
  background-color: rgb(191, 139, 228);
  border: none;
  padding: 1em;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  cursor: pointer;
}
</style>