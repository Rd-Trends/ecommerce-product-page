<template>
  <div class="image-wrapper" :style="{ borderRadius, width: width }">
    <div v-if="overlay" class="overlay" :style="{ borderRadius }"></div>
    <img :src="src" :alt="alt" :style="{ borderRadius }" />
  </div>
</template>
<script>
export default {
  name: "ImageComponenet",
  props: {
    src: String,
    alt: String,
    borderRadius: {
      type: String,
      default: "0px",
    },
    overlay: {
      type: Boolean,
      default: false,
    },
    width: String,
  },
};
</script>
<style lang="scss" scoped>
.image-wrapper {
  position: relative;
}
.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(250, 250, 250, 0.7);
  border: 3px solid var(--Orange);
}
</style>