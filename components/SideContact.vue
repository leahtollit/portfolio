<template>
  <div class="sideContact">
    <div class="sideContact__holder flex flex--dir-c alignI--center">
      <a class="sideContact__copy fc--green" href="mailto:leahtollit@gmail.com">leahtollit@gmail.com</a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SideContact',
  props: {
    options: {
      type: Object,
      default: null
    },
    margin: {
      type: String,
      default: ''
    },
    children: {
      type: Array,
      default: null
    }
  }
}
</script>

<style lang="scss">
.sideContact {
  position: absolute;
  bottom: 0px;
  right: 80px;
  z-index: 10;
  background: none;
  border: none;
  width: 40px;

  &::after {
    content: '';
    display: block;
    width: 2px;
    height: 90px;
    margin: 0px auto;
    background-color: $white;
    opacity: 0.7;
  }

  &__copy {
    margin: 20px auto;
    padding: 10px;
    font-size: 12px;
    line-height: 18px;
    letter-spacing: 0.1em;
    writing-mode: vertical-rl;
    transition: all 0.3s ease;
    font-family: $karla;
    color: white;
    opacity: 0.7;

    &:hover {
      color: $green;
      transform: translateY(-3px);
      opacity: 1;
    }
  }
}
//----------------------------------------//

// 1400
@include breakpoint(xxxl) {
  .sideContact {
    right: 40px;
  }
}

//----------------------------------------//
// 960
@include breakpoint(l) {
  .sideContact {
    right: 32px;
  }
}

//----------------------------------------//
// 600
@include breakpoint(s) {
  .sideContact {
    display: none;
  }
}
/*------------------------------------------*/
</style>
