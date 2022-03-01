<template>
  <div class="side-bar">
    <div class="close-side-bar-btn" @click="toggleSideBar">
      <img src="../../assets/images/icon-close.svg" alt="close-icon-btn" />
    </div>
    <nav-item v-for="(item, index) in NavData" :key="index" :name="item.name" />
  </div>
</template>
<script>
import NavItem from "./NavItems.vue";
import NavData from "./navigation";
export default {
  name: "SideBar",
  data() {
    return {
      NavData,
    };
  },
  components: {
    NavItem,
  },
  methods: {
    toggleSideBar() {
      this.$emit("toggleSideBar");
    },
  },
};
</script>
<style lang="scss">
.side-bar {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  max-width: 100%;
  width: 250px;
  height: 100vh;
  background-color: var(--White);
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding: 0rem 0;
  z-index: 3;

  a {
    font-weight: bold !important;
    padding: 1.2rem 0.5rem;
  }

  .close-side-bar-btn {
    margin: 1rem 1.1rem 2rem;
  }
}
</style>