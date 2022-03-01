<template>
  <Navbar
    :showSideBar="showSideBar"
    @toggleSideBar="toggleSideBar"
    :cart="cart"
    @delete-item-from-cart="deleteCartItem"
  />
  <router-view :cart="cart" @add-to-cart="addToCart" />
  <div :class="showSideBar ? `overlay` : ``"></div>
</template>

<script>
import Navbar from "@/components/Navigation";
export default {
  components: {
    Navbar,
  },
  data() {
    return {
      showSideBar: false,
      cart: [],
    };
  },
  methods: {
    toggleSideBar() {
      this.showSideBar = !this.showSideBar;
    },
    addToCart(cartItem) {
      const cartIndex = this.cart.findIndex(
        (cart) => cart.Image == cartItem.Image
      );
      if (cartIndex !== -1) {
        return this.cart;
      }
      this.cart = [...this.cart, cartItem];
    },
    deleteCartItem(itemIndex) {
      return (this.cart = this.cart.filter((item, index) => {
        return index !== itemIndex;
      }));
    },
  },
  // emits: ["add-to-cart", "deleteCartItem"],
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Kumbh+Sans:wght@400;700&display=swap");

// variables
:root {
  --Orange: hsl(26, 100%, 55%);
  --Pale-orange: hsl(25, 100%, 94%);
  --Very-dark-blue: hsl(220, 13%, 13%);
  --Dark-grayish-blue: hsl(219, 9%, 45%);
  --Grayish-blue: hsl(220, 14%, 75%);
  --Light-grayish-blue: hsl(223, 64%, 98%);
  --White: hsl(0, 0%, 100%);
  --Black: hsl(0, 0%, 0%);
  --large-padding: 0rem 10rem;
  --meduim-padding: 0rem 5rem;
  --small-padding: 0rem 1rem;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Kumbh Sans", sans-serif;
}
body {
  max-width: 100vw;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 100vw;
  padding: 0rem;
}

img {
  width: 100%;
}

h1,
h2,
h3,
h4 {
  color: var(--Very-dark-blue);
}

.overlay {
  background-color: rgba(0, 0, 0, 0.5);
  width: 100vw;
  height: 100vh;
  z-index: 2;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

@media screen and (min-width: 768px) {
  #app {
    padding: var(--meduim-padding);
  }
}

@media screen and (min-width: 1024px) {
  #app {
    padding: var(--large-padding);
  }
}

// nav {
//   padding: 30px;

//   a {
//     font-weight: bold;
//     color: #2c3e50;

//     &.router-link-exact-active {
//       color: #42b983;
//     }
//   }
// }
</style>
