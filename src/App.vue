<template>
  <div class="homepage">
    <div class="nav-app">
      <nav-links></nav-links>
      <the-cart :cart="cart" @cart-state="cartState"></the-cart>
    </div>
    <div class="product">
      <the-image-grid></the-image-grid>
      <div class="text">
        <text-content @items-to-cart="itemsToCart"></text-content>
      </div>
    </div>
  </div>
  <the-attribution></the-attribution>
</template>

<script>
import TheCart from "./components/nav/TheCart.vue";
import NavLinks from "./components/nav/NavLinks.vue";
import TheImageGrid from "./components/TheImageGrid.vue";
import TextContent from "./components/TextContent.vue";
import TheAttribution from "./components/TheAttribution.vue";
export default {
  components: {
    NavLinks,
    TheCart,
    TheImageGrid,
    TextContent,
    TheAttribution,
  },
  data() {
    return {
      itemsPassed: null,
      cart: [],
    };
  },
  methods: {
    cartState(state) {
      this.cart = state;
      // console.log(this.cart);
    },
    itemsToCart(item) {
      this.cart.push(item);
      if (this.itemsPassed === 0) return;
      console.log(this.itemsProduct, item);
      if(this.cart.length > 1) {
        this.cart.shift() 
      }
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Kumbh+Sans:wght@400;700&display=swap");

@mixin tablet {
  @media only screen and(min-width: 851px) {
    @content;
  }
}
@mixin desktop {
  @media only screen and(min-width: 1000px) {
    @content;
  }
}

#app {
  position: relative;
  font-size: 16px;
  font-family: "Kumbh Sans", sans-serif;
  width: 100%;
  min-height: 100vh;

  //overlay teleported from TheCart component
  .overlay-cart-open {
    position: absolute;
    left: 50%;
    top: 0;
    bottom: 0;
    transform: translateX(-50%);
    width: 100%;
    background-color: rgba(0, 0, 0, 0.027);
    z-index: 5;
    cursor: pointer;
  }

  .homepage {
    position: relative;
    width: 100%;
    margin: auto;
    .nav-app {
      width: 100%;
      display: flex;
      align-items: center;
      margin: auto;
      padding: 18px 20px;
      background-color: #fff;
    }
    .product {
      .text {
        width: 90%;
        max-width: 400px;
        margin: auto;
        margin-top: 20px;
        margin-bottom: 60px;
      }
    }
    @include tablet {
      width: min(90%, 1100px);
      .nav-app {
        align-items: flex-start;
        padding: 20px 20px 0 20px;
        border-bottom: 1px solid lighten(hsl(219, 9%, 45%), 45%);
      }
    }
    @include desktop {
      .product {
        margin: auto;
        margin-top: 50px;
        max-width: 900px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        .text {
          margin: unset;
        }
      }
    }
  }
}
</style>
