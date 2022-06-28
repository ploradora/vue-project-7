<template>
  <div class="user-profile">
    <div class="cart-user">
      <div class="cart-container">
        <p v-if="cart.length" class="cart-items-index">
          {{ cart.length }}
        </p>
        <img
          @click="openCart"
          class="icon-cart"
          src="../../assets/images/icon-cart.svg"
          alt="icon cart"
        />
      </div>
      <img
        class="profile-picture"
        src="../../assets/images/image-avatar.png"
        alt="profile picture"
      />
    </div>
    <div class="inside-cart-items" v-if="cartVisible">
      <p>Cart</p>
      <p v-if="cart.length === 0" class="empty">Your cart is empty.</p>
      <div class="items-container">
        <div class="item" v-for="(item, index) in cart" :key="index">
          <img
            class="item-thumbnail"
            src="../../assets/images/image-product-1-thumbnail.jpg"
            :alt="item.alt"
          />
          <div class="item-details">
            <p class="name">{{ item.name }}</p>
            <p class="price">
              ${{ item.currentPrice }} x {{ item.items }}
              <span class="total">${{ item.total }}</span>
            </p>
          </div>
          <img
            @click="deleteItem(item.id)"
            class="delete-icon"
            src="../../assets/images/icon-delete.svg"
            alt="icon delete"
          />
        </div>
        <button v-if="cart.length > 0">Checkout</button>
      </div>
    </div>
    <teleport to="#app">
      <div
        v-if="cartVisible"
        @click="closeCartOverlay"
        class="overlay-cart-open"
      ></div>
    </teleport>
  </div>
</template>

<script>
export default {
  emits: ["cart-state"],
  props: ["cart"],
  data() {
    return {
      cartVisible: false,
      clearArr: [],
    };
  },
  methods: {
    openCart() {
      this.cartVisible = !this.cartVisible;
    },
    closeCartOverlay() {
      this.cartVisible = false;
    },

    deleteItem() {
      this.$emit("cart-state", this.clearArr);
    },
  },
};
</script>

<style scoped lang="scss">
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

.user-profile {
  margin-left: auto;
  .cart-user {
    display: flex;
    align-items: center;
    .cart-container {
      position: relative;
      padding: 8px 5px 5px 5px;
      margin-right: 15px;
      z-index: 5;
      cursor: pointer;
      .cart-items-index {
        position: absolute;
        top: 3px;
        right: 0;
        width: 18px;
        font-size: 10px;
        color: #fff;
        font-weight: 700;
        text-align: center;
        border-radius: 30px;
        background-color: hsl(26, 100%, 55%);
      }
    }
    .profile-picture {
      width: 25px;
      border-radius: 50%;
      cursor: pointer;
      transition: all 0.15s linear;
      z-index: 5;
      &:hover {
        box-shadow: 0 0 0 2px hsl(26, 100%, 55%);
      }
    }
  }
  .inside-cart-items {
    position: absolute;
    width: 95%;
    max-width: 357px;
    left: 50%;
    top: 81px;
    transform: translateX(-50%);
    box-shadow: 0 8px 14px rgba(0, 0, 0, 0.2);
    border-radius: 10px;
    background-color: #fff;
    z-index: 6;
    &::after {
      position: absolute;
      content: "";
      width: 100%;
      top: 60px;
      height: 1px;
      background-color: lighten(hsl(219, 9%, 45%), 45%);
    }
    > p {
      font-weight: 700;
      padding: 20px;
    }
    .empty {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 188.44px;
      padding: unset;
      text-align: center;
      color: hsl(219, 9%, 45%);
    }
    .items-container {
      padding: 25px 20px;
      .item {
        display: flex;
        align-items: center;
        justify-content: space-between;
        flex-wrap: wrap;
        margin-bottom: 20px;
        .item-thumbnail {
          width: 60px;
          border-radius: 5px;
        }
        .item-details {
          font-size: 16px;
          font-weight: 700;
          color: hsl(219, 9%, 45%);
          .name {
            width: 210px;
            white-space: nowrap;
            margin-bottom: 7px;
            overflow: hidden;
            text-overflow: ellipsis;
          }
          .price {
            .total {
              color: #000;
            }
          }
        }
        .delete-icon {
          cursor: pointer;
        }
      }
      button {
        font-size: 16px;
        width: 100%;
        padding: 20px;
        border: none;
        font-weight: 700;
        border-radius: 10px;
        color: #fff;
        background-color: hsl(26, 100%, 55%);
        cursor: pointer;
        &:hover {
          background-color: lighten(hsl(26, 100%, 55%), 7%);
        }
      }
    }
  }
  @include tablet {
    .cart-user {
      .cart-container {
        margin-right: 30px;
      }
      .profile-picture {
        width: 42px;
      }
    }
    .inside-cart-items {
      left: unset;
      transform: unset;
      right: 0;
    }
  }
  @include desktop {
    .inside-cart-items {
      left: unset;
      transform: unset;
    }
  }
}
</style>
