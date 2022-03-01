<template>
  <div class="cart">
    <p class="cart-title">cart</p>
    <div class="cart-item" v-for="(cartItem, index) in cart" :key="index">
      <Image
        :src="require(`../../assets/images/${cartItem.thumbnail}`)"
        alt="cart item image"
        width="15%"
        borderRadius="5px"
      />
      <div class="product-details">
        <p class="product-name">{{ cartItem.productName }}</p>
        <div class="price-quantity-total">
          <p class="price-quantity">
            {{ `$${cartItem.price.toFixed(2)} x ${cartItem.quantity}` }}
          </p>
          <p class="total">
            {{ `$${(cartItem.price * cartItem.quantity).toFixed(2)}` }}
          </p>
        </div>
      </div>
      <div class="delete-btn" @click="deleteCartItem(index)">
        <img src="../../assets/images/icon-delete.svg" alt="" />
      </div>
    </div>
    <div class="cart-empty-display" v-if="cart.length <= 0">
      <p>Your cart is empty</p>
    </div>
    <div class="btn-wrapper" v-if="cart.length > 0">
      <Button @onClick="checkOut"><p>Checkout</p></Button>
    </div>
  </div>
</template>
<script>
import Image from "@/components/Image";
import Button from "@/components/Button";

export default {
  name: "CartWrapper",
  components: {
    Image,
    Button,
  },
  props: {
    cart: Array,
  },
  data() {
    return {};
  },
  methods: {
    checkOut() {
      alert("hello");
    },
    deleteCartItem(index) {
      this.$emit("delete-cart-item", index);
    },
  },
  emits: ["delete-cart-item"],
  mounted() {},
};
</script>
<style lang="scss">
.cart {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: space-between;
  border-radius: 5px;
  box-shadow: 0px 10px 30px rgba(220, 220, 221, 0.3);
  max-width: 100%;
  min-width: 250px;
  width: 300px;
  padding: 0.5rem 0rem;
  background: var(--White);

  .cart-title {
    padding: 1rem;
    display: block !important;
    width: 100%;
    text-align: left;
    border-bottom: 0.5px solid var(--Grayish-blue);
  }

  .cart-item {
    display: flex;
    align-items: center;
    padding: 1rem;
    position: relative;

    .delete-btn {
      position: absolute;
      right: 1rem;
    }

    .product-details {
      padding-left: 1rem;
      display: flex;
      flex-direction: column;
      align-items: flex-start;

      .price-quantity-total {
        display: flex;
        align-items: center;

        .price-quantity {
          font-size: 14px;
        }

        .total {
          font-weight: bold;
          padding-left: 1rem;
          color: var(--Very-dark-blue);
        }
      }

      .product-name {
        font-size: 14px;
        padding-bottom: 0.3rem;
        color: var(--Dark-greyish-blue);
      }
    }
  }

  .cart-empty-display {
    height: 150px;
    width: 100%;
    display: grid;
    place-items: center;
  }

  .btn-wrapper {
    width: 100%;
    padding: 0rem 1rem 1rem;
  }
}
@media screen and (max-width: 768px) {
  .cart {
    width: 90vw;
    margin: 0 auto;
  }
}
</style>