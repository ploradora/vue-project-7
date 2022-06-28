<template>
  <div class="arrows-mobile">
    <div class="left" @click="$emit('prev')">
      <img
        class="icon-left"
        src="../../assets/images/icon-previous.svg"
        alt="icon arrow left"
      />
    </div>
    <div class="right" @click="$emit('next')">
      <img
        class="icon-right"
        src="../../assets/images/icon-next.svg"
        alt="icon arrow right"
      />
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style scoped lang="scss">
@mixin grid-enter {
  @media only screen and(min-width: 502px) {
    @content;
  }
}
.arrows-mobile {
  width: 90%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  align-items: center;
  justify-content: space-between;
  user-select: none;
  z-index: 2;
  .left,
  .right {
    background-color: #fff;
    width: 35px;
    height: 35px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    position: relative;
    cursor: pointer;
    .icon-left {
      left: 47%;
    }
    .icon-right {
      left: 52%;
    }
    img {
      position: absolute;
      width: 9px;
      display: block;
      top: 50%;
      transform: translate(-50%, -50%);
      pointer-events: none;
    }
  }
  @include grid-enter {
    display: none;
  }
}
</style>
