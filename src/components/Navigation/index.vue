<template >
  <nav>
    <div class="nav-items-logo-wrapper">
      <button class="sidebar-toggler" @click="toggleSideBar">
        <img
          src="../../assets/images/icon-menu.svg"
          alt="navigator menu toggler"
        />
      </button>
      <div class="logo">
        <img src="../../assets/images/logo.svg" alt="sneakers brand logo" />
      </div>
      <div class="nav-items">
        <nav-item
          v-for="(item, index) in NavData"
          :key="index"
          :name="item.name"
          height="5rem"
        />
      </div>
    </div>
    <div class="cart-menu">
      <div class="cart-icon" ref="cartIcon" @click="toggleShowCart">
        <div v-if="cart.length > 0" class="cart-total-quantity">
          {{ calculateCartTotal }}
        </div>
        <img src="../../assets/images/icon-cart.svg" alt="cart icon" />
      </div>
      <div class="user">
        <img src="../../assets/images/image-avatar.png" alt="user image" />
      </div>
    </div>
    <transition name="cart">
      <div class="cart-wrapper" ref="cartWrapper" v-show="showCart">
        <Cart :cart="cart" @delete-cart-item="deleteItemFromCart" />
      </div>
    </transition>
  </nav>
  <transition name="sidebar">
    <side-bar v-if="showSideBar" @toggleSideBar="toggleSideBar" />
  </transition>
</template>

<script>
//  **import components
import NavItem from "./NavItems.vue";
import NavData from "./navigation";
import SideBar from "./SideBar.vue";
import Cart from "@/components/Cart";

console.log(NavData);

export default {
  name: "NavigationBar",
  components: {
    NavItem,
    Cart,
    SideBar,
  },
  props: {
    showSideBar: Boolean,
    cart: Array,
  },
  data() {
    return {
      NavData,
      showCart: false,
    };
  },
  methods: {
    toggleShowCart() {
      this.showCart = !this.showCart;
    },
    toggleSideBar() {
      this.$emit("toggleSideBar");
    },
    setCartPosition() {
      const cartIemPosition = this.$refs.cartIcon.getBoundingClientRect();
      const cartCenter = (cartIemPosition.left + cartIemPosition.right) / 2;
      // console.log(this.$refs.cartWrapper, cartCenter)
      if (window.innerWidth > 768) {
        this.$refs.cartWrapper.style.left = `${cartCenter - 150}px`;
        console.log(this.$refs.cartWrapper.getBoundingClientRect().width);
      }
    },
    deleteItemFromCart(index) {
      this.$emit("delete-item-from-cart", index);
    },
  },
  computed: {
    calculateCartTotal() {
      return this.cart.length > 0
        ? this.cart.reduce((total, num) => {
            return total + num.quantity;
          }, 0)
        : "0";
    },
  },
  emits: ["toggleSideBar", "delete-item-from-cart"],
  watch: {
    showCart(newValue) {
      if (newValue && this.$refs.cartWrapper) {
        this.setCartPosition();
      }
    },
  },
  mounted() {
    // console.log(this.$refs.cartWrapper.getBoundingClientRect().width);
  },
};
</script>

<style lang="scss" scoped>
nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1px solid var(--Grayish-blue);

  .logo {
    margin-right: 5rem;
    @media screen and (max-width: 768px) {
      margin-right: 1rem;
    }
  }

  .nav-items-logo-wrapper {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .sidebar-toggler {
    background-color: transparent;
    outline: none;
    padding: 0.5rem;
    border: none;
    display: flex;
    align-items: center;
  }

  .nav-items {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .cart-menu {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-left: 1rem !important;

    .cart-icon {
      cursor: pointer;
      position: relative;

      .cart-total-quantity {
        position: absolute;
        right: -5px;
        top: -5px;
        display: flex;
        align-items: center;
        justify-content: center;
        width: 17px;
        height: 17px;
        font-size: 12px;
        border-radius: 100%;
        color: var(--White);
        background-color: var(--Orange);
      }
    }

    .user {
      margin-left: 1.5rem;
      border-radius: 50%;
      background: #000;
      border: 3px solid var(--Orange);

      img {
        width: 30px;
      }
    }
  }
  .cart-wrapper {
    position: absolute;
    top: 4rem;
    z-index: 2;
    left: 0;
    right: 0;
  }
}

.cart-enter-active,
.cart-leave-active {
  transition: opacity 0.5s ease;
}

.cart-enter-from,
.cart-leave-to {
  opacity: 0;
}

.sidebar-enter-active,
.sidebar-leave-active {
  transition: transform 0.5s ease;
  // transform: translateX(0);
}

.sidebar-enter-from,
.sidebar-leave-to {
  transform: translateX(-300px);
}

@media screen and (max-width: 768px) {
  nav {
    padding: 1rem 1rem 1rem 0.5rem;
    border: none;

    .nav-items {
      display: none !important;
    }
  }

  .cart-wrapper {
    top: 5rem !important;
  }
}

@media screen and (min-width: 768px) {
  .sidebar-toggler {
    display: none !important;
  }
}
</style>