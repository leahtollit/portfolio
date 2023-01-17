<template>
  <header class="globalHeader pos--fix z--max" :class="{ 'globalHeader--collapsed': collapsed }">
    <div class="globalHeader__container container flex justifyC--between">
      <a href="" class="globalHeader__logo">Logo</a>
      <div class="globalHeader__navItems flex alignI--center">
        <ul class="globalHeader__nav flex">
          <li class="globalHeader__navItem">
            <a href="" @click.prevent="scrollToElement('#about')">01. <span>About</span></a>
          </li>
          <li class="globalHeader__navItem">
            <a href="" @click.prevent="scrollToElement('#experience')">02. <span>Experience</span></a>
          </li>
          <li class="globalHeader__navItem">
            <a href="" @click.prevent="scrollToElement('#work')">03. <span>Work</span></a>
          </li>
          <li class="globalHeader__navItem">
            <a href="" @click.prevent="scrollToElement('#contact')">04. <span>Contact</span></a>
          </li>
        </ul>
        <BaseBtn class="baseBtn globalHeader__button" :link="``">Resume</BaseBtn>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'GlobalHeader',
  data() {
    return {
      collapsed: false
    }
  },
  mounted() {
    window.addEventListener('scroll', () => {
      if (window.scrollY > 10) {
        this.collapsed = true
      } else {
        this.collapsed = false
      }
    })
  },
  methods: {
    scrollToElement(element) {
      const offset = document.querySelector(element).offsetTop
      const headerHeight = document.querySelector('.globalHeader').clientHeight

      window.scrollTo({
        top: offset - headerHeight,
        behavior: 'smooth'
      })
    }
  }
}
</script>

<style lang="scss">
.globalHeader {
  padding: 42px 0;
  margin: 0 0 40px;
  top: 0;
  right: 0;
  left: 0;
  transition: padding 0.3s ease, opacity 0.3s ease, background 0.3s ease;

  &--collapsed {
    padding: 21px 0;
    background: $bg;
  }

  &__navItem {
    margin-right: 12px;
    list-style: none;
    margin: 0px 5px;
    padding: 10px;
    font-size: 16px;
    line-height: 16.9px;
    font-weight: 500;
    font-family: $karla;
    color: white;

    &:hover {
      span {
        color: $green;
      }
    }

    &:nth-last-of-type(1) {
      margin-right: 0;
    }
  }
  span {
    transition: color 0.3s ease;
  }
}

//----------------------------------------//

// 960
@include breakpoint(l) {
  .globalHeader {
    &__nav {
      display: none;
    }
  }
}
</style>
