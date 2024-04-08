<script>
import { RouterView } from 'vue-router';


export default {
  data() {
    return {
      
    };
  }
};
</script>

<template>
  <div>
    <RouterView/>
  </div>
</template>

<style>
  @font-face {
    font-family: "Avenir";
    src: local("Avenir"),
    url(./assets/font/AvenirLTStd-Book.otf) format("truetype");

  }

  body{
    margin: 0;
    box-sizing: border-box;
    background-image: url('../src/assets/BG.png');
    background-size: cover;
    font-family: 'Avenir';
  }
</style>
