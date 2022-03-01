<template>
  <div class="product">
    <div class="product-hero-image">
      <Image
        px="0rem"
        py="0rem"
        :borderRadius="setBorderRadius()"
        :src="require(`../assets/images/${product[productItemIndex].Image}`)"
        @click="toggleLightBoxGallery"
      />
      <div class="previous-btn">
        <Button
          width="40px"
          borderRadius="100%"
          py="0.8rem"
          px="0.9rem"
          bgColor="var(--White)"
          @onClick="setPreviousImage"
        >
          <img src="../assets/images/icon-previous.svg" alt="" />
        </Button>
      </div>
      <div class="next-btn">
        <Button
          width="40px"
          borderRadius="100%"
          py="0.8rem"
          px="0.9rem"
          bgColor="var(--White)"
          @onClick="setNextImage"
        >
          <img src="../assets/images/icon-next.svg" alt="" />
        </Button>
      </div>
      <div class="thumbnails">
        <Image
          v-for="(item, index) in product"
          :key="index"
          px="0rem"
          py="0rem"
          :src="require(`../assets/images/${item.thumbnail}`)"
          borderRadius="10px"
          :overlay="index === productItemIndex ? true : false"
          @click="productItemIndex = index"
        />
      </div>
    </div>
    <div class="product-details">
      <p class="company-name">sneaker company</p>
      <h1 class="product-title">
        {{ product[productItemIndex].productName }}
      </h1>
      <p class="product-description">
        {{ product[productItemIndex].description }}
      </p>
      <div class="prices">
        <div>
          <span class="price">{{
            "$" + product[productItemIndex].price.toFixed(2)
          }}</span>
          <span class="discount">
            {{
              (product[productItemIndex].price /
                product[productItemIndex].initialPrice) *
                100 +
              "%"
            }}
          </span>
        </div>
        <small>{{ "$" + product[productItemIndex].initialPrice }}</small>
      </div>
      <div class="CTA">
        <div class="quantity-btn">
          <Button
            width="40px"
            bgColor="transparent"
            @onClick="decreaseQuantity"
          >
            <img src="../assets/images/icon-minus.svg" alt="" />
          </Button>
          <p>{{ product[productItemIndex].quantity }}</p>
          <Button
            width="40px"
            bgColor="transparent"
            @onClick="increaseQuantity"
          >
            <img src="../assets/images/icon-plus.svg" alt="" />
          </Button>
        </div>

        <Button width="100%" @onClick="addToCart">
          <div class="add-to-cart-btn">
            <img src="../assets/images/icon-cart.svg" alt="cart icon" />
            <p>Add to cart</p>
          </div>
        </Button>
      </div>
    </div>
  </div>

  <LightBoxGallery
    v-if="showLightBoxGallery"
    :product="product"
    :productItemIndex="productItemIndex"
    @set-next-image="setNextImage"
    @set-previous-image="setPreviousImage"
    @change-display-image="changeDisplayImage"
    @close-lightbox-gallery="toggleLightBoxGallery"
  />
</template>

<script>
// @ is an alias to /src
import Image from "@/components/Image";
import Button from "@/components/Button";
import LightBoxGallery from "@/components/LightBoxGallery";

export default {
  name: "HomeView",
  components: {
    Image,
    Button,
    LightBoxGallery,
  },
  props: {
    cart: Array,
  },
  data() {
    return {
      product: [
        {
          productName: "Fall Limited Edition Sneakers",
          description: `These low profile sneakers are your perfect casual 
          wear companion. Featuring a durable outer sole. They will withstand 
          everything the weather can offer `,
          Image: "image-product-1.jpg",
          thumbnail: "image-product-1-thumbnail.jpg",
          price: 125.0,
          initialPrice: 250,
          quantity: 0,
        },
        {
          productName: "Fall Limited Edition Sneakers",
          description: `These low profile sneakers are your perfect casual 
          wear companion. Featuring a durable outer sole. They will withstand 
          everything the weather can offer `,
          Image: "image-product-2.jpg",
          thumbnail: "image-product-2-thumbnail.jpg",
          price: 125.0,
          initialPrice: 250,
          quantity: 0,
        },
        {
          productName: "Fall Limited Edition Sneakers",
          description: `These low profile sneakers are your perfect casual 
          wear companion. Featuring a durable outer sole. They will withstand 
          everything the weather can offer `,
          Image: "image-product-3.jpg",
          thumbnail: "image-product-3-thumbnail.jpg",
          price: 125.0,
          initialPrice: 250,
          quantity: 0,
        },
        {
          productName: "Fall Limited Edition Sneakers",
          description: `These low profile sneakers are your perfect casual 
          wear companion. Featuring a durable outer sole. They will withstand 
          everything the weather can offer `,
          Image: "image-product-4.jpg",
          thumbnail: "image-product-4-thumbnail.jpg",
          price: 125.0,
          initialPrice: 250,
          quantity: 0,
        },
      ],
      productItemIndex: 0,
      windowWidth: window.innerWidth,
      showLightBoxGallery: false,
    };
  },
  created() {
    console.log("created");
  },
  methods: {
    setNextImage() {
      if (this.productItemIndex != this.product.length - 1) {
        this.productItemIndex++;
      }
    },
    setPreviousImage() {
      if (this.productItemIndex !== 0) {
        this.productItemIndex--;
      }
    },
    changeDisplayImage(index) {
      this.productItemIndex = index;
      // console.log(index);
    },
    setBorderRadius() {
      return window.innerWidth >= 768 ? "20px" : "0rem";
    },
    increaseQuantity() {
      this.product[this.productItemIndex].quantity++;
    },
    decreaseQuantity() {
      if (this.product[this.productItemIndex].quantity <= 0) {
        return;
      }
      this.product[this.productItemIndex].quantity--;
    },
    addToCart() {
      if (this.product[this.productItemIndex].quantity > 0) {
        this.$emit("add-to-cart", this.product[this.productItemIndex]);
      }
    },
    toggleLightBoxGallery() {
      if (window.innerWidth >= 768) {
        this.showLightBoxGallery = !this.showLightBoxGallery;
      }
      return;
    },
  },
  emits: ["add-to-cart"],
};
</script>


<style scoped lang="scss">
.product-hero-image {
  position: relative;
}

.next-btn,
.previous-btn {
  position: absolute;
  transform: translateY(-50%);
  @media screen and (min-width: 768px) {
    display: none;
  }
}
.next-btn {
  right: 1rem;
  top: 50%;
}
.previous-btn {
  left: 1rem;
  top: 50%;
}
.thumbnails {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 1rem;
  align-items: center;
  margin-top: 1rem;

  @media screen and (max-width: 767px) {
    display: none;
  }
}

.product-details {
  padding: 1rem;
  text-align: left;

  > * {
    margin-bottom: 1rem;
  }
  .company-name {
    font-size: 12px;
    font-weight: bold;
    color: var(--Orange);
    text-transform: uppercase;
  }
  .product-description {
    color: var(--Dark-grayish-blue);
    line-height: 2rem;
  }

  .prices {
    display: flex;
    align-items: center;
    justify-content: space-between;

    div {
      display: flex;
      align-items: center;
    }

    small {
      text-decoration: line-through;
      color: var(--Dark-grayish-blue);
      font-size: 16px;
    }

    .price {
      color: var(--Very-dark-blue);
      font-weight: bold;
      font-size: 36px;
      margin-right: 1rem;
    }
    .discount {
      background-color: var(--Pale-orange);
      color: var(--Orange);
      padding: 0.6rem 0.8rem;
      border-radius: 5px;
    }
  }
  .quantity-btn {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: var(--Light-grayish-blue);
    margin-bottom: 1rem;
    border-radius: 10px;

    p {
      font-weight: bold;
      color: var(--Very-dark-blue);
    }
  }

  .add-to-cart-btn {
    display: flex;
    align-items: center;
    justify-content: center;

    img {
      margin-right: 1rem;
      width: 20px;
    }
  }
}

@media screen and (min-width: 768px) {
  .product {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 4rem 4rem;

    @media screen and (min-height: 800px) {
      height: calc(100vh - 80px);
    }

    .product-hero-image {
      margin-right: 5rem;
    }

    .CTA {
      display: flex;
      align-items: center;
      margin-top: 2rem;

      .quantity-btn {
        width: 80%;
        margin-right: 1rem;
        margin-bottom: 0;
      }
    }
  }
}

@media screen and (min-width: 768px) and (max-width: 1024px) {
  .product {
    padding:4rem 1rem;
  }
}
</style>

