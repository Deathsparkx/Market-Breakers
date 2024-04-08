<template>
    <div class="image-container">
        <img :src="imageUrl" alt="My Image" class="left-aligned">
    </div>
</template>

<script>
export default {
    data() {
        return {
        imageUrl: '//assets/BG.png' // Relative path to your image
        };
    }
};
</script>

<style>
.image-container {
  margin: 0; /* Remove margin */
  padding: 0; /* Remove padding */
  max-width: none; /* Remove max-width constraint */
}

.left-aligned {
  display: block; /* Ensure the image behaves as a block element */
  margin-right: auto; /* Align to the left by setting margin-right to auto */
}
</style>