<!-- level 1 child -->

<template>
  <p class="company">SNEAKER COMPANY</p>
  <h1>Fall Limited Edition Sneakers</h1>
  <p class="main-text">
    These low-profile sneakers are your perfect casual wear companion. Featuring
    a durable rubber outer sole, they’ll withstand everything the weather can
    offer.
  </p>
  <div class="price">
    <div class="current-price">
      <p id="current-price">${{ currentPrice }}</p>
      <p class="discount">{{ discount }}%</p>
    </div>
    <p class="previous-price">${{ price.toFixed(2) }}</p>
  </div>
  <div class="buttons">
    <div class="calc-buttons-container">
      <button class="calc subtract" @click="subtract">-</button>
      <div class="items">{{ items }}</div>
      <button class="calc add" @click="add">+</button>
    </div>
    <button @click="addToCart" class="add-to-cart">
      <svg width="22" height="20" xmlns="http://www.w3.org/2000/svg">
        <path
          d="M20.925 3.641H3.863L3.61.816A.896.896 0 0 0 2.717 0H.897a.896.896 0 1 0 0 1.792h1l1.031 11.483c.073.828.52 1.726 1.291 2.336C2.83 17.385 4.099 20 6.359 20c1.875 0 3.197-1.87 2.554-3.642h4.905c-.642 1.77.677 3.642 2.555 3.642a2.72 2.72 0 0 0 2.717-2.717 2.72 2.72 0 0 0-2.717-2.717H6.365c-.681 0-1.274-.41-1.53-1.009l14.321-.842a.896.896 0 0 0 .817-.677l1.821-7.283a.897.897 0 0 0-.87-1.114ZM6.358 18.208a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm10.015 0a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm2.021-7.243-13.8.81-.57-6.341h15.753l-1.383 5.53Z"
          fill="#69707D"
          fill-rule="nonzero"
        />
      </svg>
      Add to cart
    </button>
  </div>
</template>

<script>
export default {
  emits: ["itemsToCart"],
  data() {
    return {
      item: {
        alt: "leather shoes",
        name: "Autumn Limited Edition Sneakers",
        currentPrice: null,
        items: null,
        total: null,
        id: 1,
      },
      items: 0,
      price: 250,
      discount: 50,
      total: null,
    };
  },
  computed: {
    currentPrice() {
      const calcPerc = this.price * this.discount;
      const theDiscount = calcPerc / 100;
      const currentPrice = (this.price - theDiscount).toFixed(2);
      return currentPrice;
    },
  },
  methods: {
    subtract() {
      if (this.items <= 0) {
        return;
      } else {
        this.items--;
      }
    },
    add() {
      this.items++;
    },
    addToCart() {
      if (this.items === 0) {
        return;
      } else {
        const total = this.currentPrice * this.items;
        this.item.total = total.toFixed(2);
        this.item.items = this.items;
        this.item.currentPrice = this.currentPrice;
        this.$emit("itemsToCart", this.item);
        this.items = 0;
      }
    },
  },
};
</script>

<style scoped lang="scss">
@mixin button-brake {
  @media only screen and(min-width: 600px) {
    @content;
  }
}
@mixin tablet {
  @media only screen and(min-width: 850px) {
    @content;
  }
}
@mixin desktop {
  @media only screen and(min-width: 1000px) {
    @content;
  }
}

.company {
  font-size: 13px;
  font-weight: 700;
  letter-spacing: 1px;
  margin-bottom: 10px;
  color: hsl(26, 100%, 55%);
}
h1 {
  width: 90%;
  font-size: 28px;
  line-height: 28px;
}
.main-text {
  margin-top: 15px;
  margin-bottom: 20px;
  font-size: 15px;
  line-height: 20px;
  color: hsl(219, 9%, 45%);
}
.price {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 20px;
  .current-price {
    width: 155px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    #current-price {
      font-size: 28px;
      font-weight: 700;
    }
    .discount {
      padding: 2px 5px 2px 6px;
      border-radius: 4px;
      font-weight: 700;
      font-size: 15px;
      color: hsl(26, 100%, 55%);
      background-color: lighten(hsl(26, 100%, 55%), 25%);
    }
  }
  .previous-price {
    text-decoration: line-through;
    font-size: 15px;
    font-weight: 700;
    color: hsl(220, 14%, 75%);
  }
}
.buttons {
  padding-bottom: 15px;
  button {
    font-family: "Kumbh Sans", sans-serif;
    height: 60.4px;
    border: unset;
  }
  .calc-buttons-container {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 15px;
    border-radius: 5px;
    background-color: lighten(hsl(220, 14%, 75%), 19%);
    .calc {
      width: 67px;
      font-size: 30px;
      font-weight: 700;
      padding-bottom: 5px;
      color: hsl(26, 100%, 55%);
      background-color: lighten(hsl(220, 14%, 75%), 19%);
      cursor: pointer;
      &:hover {
        background-color: hsl(218, 16%, 86%);
      }
    }
    .add {
      border-radius: 0 5px 5px 0;
    }
    .subtract {
      border-radius: 5px 0 0 5px;
    }
    .items {
      display: flex;
      align-items: center;
      font-weight: 700;
    }
  }
  .add-to-cart {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 700;
    font-size: 15px;
    border-radius: 5px;
    color: #fff;
    background-color: hsl(26, 100%, 55%);
    box-shadow: 0 20px 19px -3px hsla(26, 100%, 55%, 0.459);
    cursor: pointer;
    &:hover {
      background-color: lighten(hsl(26, 100%, 55%), 10%);
    }
    svg {
      margin-right: 15px;
      path {
        fill: #fff;
      }
    }
  }
}
@media only screen and (min-width: 501px) {
  h1 {
    width: 100%;
  }
}
@include button-brake {
  .price {
    display: block;
    margin-bottom: 30px;
    .current-price {
      margin-bottom: 6px;
    }
  }
  .buttons {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    padding-bottom: 45px;
    .calc-buttons-container {
      margin-bottom: unset;
      width: unset;
      margin-right: 15px;
      flex-basis: 40%;
    }
    .add-to-cart {
      width: unset;
      flex-basis: 60%;
    }
  }
}
@include desktop {
  h1 {
    font-size: 35px;
    line-height: unset;
  }
  .main-text {
    margin-top: 25px;
    line-height: 24px;
  }
  .price {
    .current-price {
      width: 142px;
      #current-price {
        font-size: 25px;
      }
      .discount {
        font-size: 14px;
      }
    }
    .previous-price {
      font-size: 14px;
    }
  }
  .buttons {
    padding-bottom: unset;
    button {
      height: 48px;
    }
    .calc-buttons-container {
      .calc {
        width: 50px;
        font-size: 25px;
      }
      .items {
        font-size: 14px;
      }
    }
    .add-to-cart {
      font-size: 13px;
      svg {
        transform: scale(0.8);
      }
    }
  }
}
</style>
