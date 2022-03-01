<template>
  <div class="lightbox-gallery-wrapper">
    <div class="close-lightbox-btn-wrapper">
      <div class="close-lightbox">
        <Button
          bgColor="transparent"
          width="50px"
          color="var(--Orange)"
          @onClick="closeLightBoxGallery"
        >
          <svg width="14" height="15" xmlns="http://www.w3.org/2000/svg">
            <path
              d="m11.596.782 2.122 2.122L9.12 7.499l4.597 4.597-2.122 2.122L7 9.62l-4.595 4.597-2.122-2.122L4.878 7.5.282 2.904 2.404.782l4.595 4.596L11.596.782Z"
              fill="var(--Orange)"
              fill-rule="evenodd"
            />
          </svg>
        </Button>
      </div>
    </div>
    <div class="product-hero-image">
      <Image
        px="0rem"
        py="0rem"
        borderRadius="20px"
        :src="require(`../../assets/images/${product[productItemIndex].Image}`)"
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
          <img src="../../assets/images/icon-previous.svg" alt="" />
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
          <img src="../../assets/images/icon-next.svg" alt="" />
        </Button>
      </div>
      <div class="thumbnails">
        <Image
          v-for="(item, index) in product"
          :key="index"
          px="0rem"
          py="0rem"
          :src="require(`../../assets/images/${item.thumbnail}`)"
          borderRadius="10px"
          :overlay="index === productItemIndex ? true : false"
          @click="changeDisplayImage(index)"
        />
      </div>
    </div>
  </div>
</template>
<script>
import Image from "@/components/Image";
import Button from "@/components/Button";

export default {
  name: "LightBoxGallery",
  components: {
    Image,
    Button,
  },
  props: {
    product: Array,
    productItemIndex: Number,
  },
  methods: {
    setNextImage(index) {
      this.$emit("set-next-image", index);
    },
    setPreviousImage() {
      this.$emit("set-previous-image");
    },
    changeDisplayImage(index) {
      this.$emit("change-display-image", index);
    },
    closeLightBoxGallery() {
      this.$emit("close-lightbox-gallery");
    },
  },
};
</script>
<style scoped lang="scss">
.lightbox-gallery-wrapper {
  width: 100vw;
  height: 100vh;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  position: fixed;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: rgba(0, 0, 0, 0.7);
  z-index: 2;
}

.close-lightbox-btn-wrapper {
  position: relative;
  width: 30%;
  min-width: 400px;
}

.close-lightbox {
  position: absolute;
  right: -1rem;
  top: -3rem;
  z-index: 3;
}
.product-hero-image {
  width: 30%;
  min-width: 400px;
  position: relative;
}

.next-btn,
.previous-btn {
  position: absolute;
  transform: translateY(-40%);
}
.next-btn {
  right: -1rem;
  top: 40%;
}
.previous-btn {
  left: -1rem;
  top: 40%;
}
.thumbnails {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 1rem;
  align-items: center;
  margin-top: 1rem;
}
</style>