<script>
import MainUI from './components/MainUI.vue';
import myImage from './assets/BG.png';

export default {
  data() {
    return {
      myImage: myImage
    };
  }
};
</script>

<template>
  <div>
    <img :src="myImage" alt="My Image">
  </div>
</template>
