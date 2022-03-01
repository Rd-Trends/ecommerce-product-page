<template >
  <button
    :style="{
      paddingRight: px,
      paddingLeft: px,
      paddingTop: py,
      paddingBottom: py,
      color: textColor,
      backgroundColor: bgColor,
      borderRadius,
      width,
    }"
    @click.prevent.stop="onClick"
  >
    {{ btnText ? btnText : "" }}
    <slot></slot>
  </button>
</template>
<script>
export default {
  name: "CustomButton",
  props: {
    btnText: String,
    px: {
      type: String,
      default: "1rem",
    },
    py: {
      type: String,
      default: "1rem",
    },
    textColor: {
      type: String,
      default: "white",
    },
    bgColor: {
      type: String,
      default: "var(--Orange)",
    },
    borderRadius: {
      type: String,
      default: "10px",
    },
    width: {
      type: String,
      default: "100%",
    },
  },
  methods: {
    onClick() {
      this.$emit("onClick");
    },
  },
};
</script>
<style scoped lang="scss">
button {
  outline: none;
  border: none;
  display: block;
  cursor: pointer;
  // width: 100%;

  &:hover,
  &:active {
    opacity: 70%;
  }
}
</style>