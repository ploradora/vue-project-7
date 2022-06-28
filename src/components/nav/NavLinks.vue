<template>
  <nav>
    <img
      @click="openMenu"
      class="hamburger-menu"
      src="../../assets/images/icon-menu.svg"
      alt="icon menu"
    />
    <img class="logo" src="../../assets/images/logo.svg" alt="sneakers logo" />
    <div class="nav-links-container">
      <div class="nav-links" v-if="menuVisible">
        <img
          class="icon-close"
          @click="closeMenu"
          src="../../assets/images/icon-close.svg"
          alt="icon close"
        />
        <a href="#">Collections</a>
        <a href="#">Men</a>
        <a href="#">Women</a>
        <a href="#">About</a>
        <a href="#">Contact</a>
      </div>
      <div class="overlay" @click="closeMenu" v-if="menuVisible"></div>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      menuVisible: false,
    };
  },
  mounted() {
    this.resizeWindow();
    window.addEventListener("resize", this.resizeWindow);
  },
  methods: {
    openMenu() {
      this.menuVisible = true;
      this.overlay = true;
      document.body.style.overflow = "hidden";
    },
    closeMenu() {
      this.menuVisible = false;
      this.overlay = false;
      document.body.style.overflow = "unset";
    },
    resizeWindow() {
      let windowWidth = window.innerWidth;
      if (windowWidth >= 851) {
        this.menuVisible = true;
        document.body.style.overflow = "unset";
      } else {
        this.menuVisible = false;
      }
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

nav {
  .hamburger-menu {
    margin-right: 15px;
    cursor: pointer;
  }
  .nav-links-container {
    .nav-links {
      position: absolute;
      width: 70%;
      height: 100vh;
      top: 0;
      left: 0;
      bottom: 0;
      padding: 18px;
      z-index: 10;
      background-color: rgb(255, 255, 255);
      .icon-close {
        padding: 5px 5px 5px 3px;
        margin-top: 7px;
        margin-bottom: 45px;
        cursor: pointer;
      }
      a {
        display: block;
        font-weight: 700;
        text-decoration: none;
        margin-bottom: 16px;
        color: #000;
        cursor: pointer;
        &:hover {
          color: hsl(219, 9%, 45%);
        }
      }
    }
  }
  .overlay {
    position: absolute;
    min-height: 100vh;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    cursor: pointer;
    background-color: rgba(0, 0, 0, 0.75);
    z-index: 9;
  }
  @include tablet {
    display: flex;
    align-items: flex-start;
    .hamburger-menu,
    .icon-close,
    .overlay {
      display: none;
    }
    .logo {
      padding-top: 10px;
      margin-right: 40px;
    }
    .nav-links-container {
      .nav-links {
        background-color: unset;
        height: unset;
        width: unset;
        padding: unset;
        position: relative;
        display: flex;
        align-items: center;
        padding-top: 12px;
        justify-content: space-between;
        z-index: 4;
        a {
          padding-bottom: 40px;
          margin-bottom: unset;
          margin-right: 25px;
          color: hsl(219, 9%, 45%);
          &:hover {
            color: #000;
            box-shadow: inset 0 -3px hsl(26, 100%, 55%);
            transition: all 0.15s linear;
          }
        }
      }
    }
    .overlay {
      display: none;
    }
  }
}
</style>
