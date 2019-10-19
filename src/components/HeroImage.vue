<template>

  <div class="HeroImage" />

</template>

<script>
export default {
  name: 'HeroImage',
};
</script>

<style lang="scss" scoped>
.HeroImage {
  position: fixed;
  top: 0;
  z-index: -1;
  width: 100%;
  height: 100vh;
  background-image: url('../assets/heroimage.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 90% 90%;
}

.HeroImage::after {
  content: '';
  background: rgba(184, 141, 141, 0.2);
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
  width: 100%;
  height: 100vh;
}

</style>
