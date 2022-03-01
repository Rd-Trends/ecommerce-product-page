<template>
  <router-link :style="{height: height}" :to="link">{{ name }}</router-link>
</template>
<script>
export default {
  name: "NavItem",
  props: {
    name: String,
    height: String,
    link: {
      type: String,
      default: "#",
    },
  },
};
</script>
<style scoped lang="scss">
a {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding: 1rem 0.2rem;
  margin: 0 0.8rem;
  text-align: center;
  text-decoration: none;
  color: var(--black);

  &:hover,
  &:active,
  &:focus {
    font-weight: bold;
    border-bottom: 5px solid var(--Orange);
  }
}
</style>