<template>
  <div class="attribution">
    Challenge by
    <a href="https://www.frontendmentor.io/challenges/ecommerce-product-page-UPsZ9MJp6" target="_blank"
      >Frontend Mentor</a
    >. Coded by <a href="#">Sebastian Suciu</a>.
  </div>
</template>

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
.attribution {
  position: absolute;
  width: 100%;
  bottom: -50px;
  left: 50%;
  transform: translateX(-50%);
  padding-bottom: 5px;
  font-family: "Times New Roman", Times, serif;
  font-size: 13px;
  text-align: center;
  a {
    color: hsl(30, 1%, 60%);
  }
  @include desktop() {
    bottom: 5px;
  }
}
</style>
