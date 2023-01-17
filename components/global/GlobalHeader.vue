<template>
  <header class="globalHeader pos--fix z--max" :class="{ 'globalHeader--collapsed': collapsed }">
    <div class="globalHeader__container container flex justifyC--end">
      <div class="globalHeader__navItems flex alignI--center">
        <ul class="globalHeader__nav flex">
          <li class="globalHeader__navItem">
            <a class="globalHeader__navLink" href="" @click.prevent="scrollToElement('#work')"
              >01. <span>My Work</span></a
            >
          </li>
          <li class="globalHeader__navItem">
            <a class="globalHeader__navLink" href="" @click.prevent="scrollToElement('#experience')"
              >02. <span>Experience</span></a
            >
          </li>
          <li class="globalHeader__navItem">
            <a class="globalHeader__navLink" href="" @click.prevent="scrollToElement('#certifications')"
              >03. <span>Certifications</span></a
            >
          </li>
          <li class="globalHeader__navItem">
            <a class="globalHeader__navLink" href="" @click.prevent="scrollToElement('#hobbies')"
              >04. <span>Hobbies</span></a
            >
          </li>
        </ul>
        <BaseBtn
          class="baseBtn baseBtn--download baseBtn--green globalHeader__button"
          :type="`download`"
          :href="`/leah-tollit-cv.pdf`"
          >Resume</BaseBtn
        >
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
    background: $green;

    .globalHeader__navItem {
      color: $white;
    }

    .globalHeader__navLink::after {
      background: $white;
    }

    .baseBtn--green {
      border: 1px solid white;

      &:hover {
        background: hsla(180, 91%, 87%, 0.3);
      }

      .baseBtn__label {
        color: $white;
      }
    }
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
    color: $greenDark;
    transition: color 0.3s ease;

    &:nth-last-of-type(1) {
      margin-right: 0;
    }
  }
  span {
    transition: color 0.3s ease;
  }

  &__navLink {
    position: relative;

    &::after {
      position: absolute;
      content: '';
      width: 100%;
      height: 1px;
      background: $greenDark;
      left: 0;
      bottom: -2px;
      z-index: -1;
      transform: scaleX(0);
      transition: transform 0.3s cubic-bezier(0.25, 0.1, 0.25, 1);
    }

    &:hover::after {
      transform: scaleX(1);
    }
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
