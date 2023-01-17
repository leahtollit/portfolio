<template>
  <section class="bannerHero pos--rel flex alignI--end">
    <div class="bannerHero__container container flex pos--rel flex--dir-c flex--nowrap justifyC--end alignI--start">
      <h1 class="bannerHero__header flex flex--dir-c"><span>Leah Tollit</span><span>web dev</span></h1>
      <p class="bannerHero__text fs--20 fw--400 fc--white o--8 ff--karla">
        I am a Manchester-based Front End Developer. I am a hardworking, passionate, and innovative individual who is
        always up for a challenge.
      </p>
      <div class="bannerHero__buttonHolder">
        <BaseBtn
          @click.prevent="scrollToElement('#')"
          class="baseBtn bannerHero__button baseBtn--inactive z--1"
          :link="``"
          >Hire Me
        </BaseBtn>
      </div>
    </div>
    <SideContact />
  </section>
</template>

<script>
import { inview } from '~/mixins/inview.js'

export default {
  name: 'BannerHero',
  mixins: [inview],
  props: {
    label: {
      type: String,
      default: ''
    },
    options: {
      type: Array,
      default: null
    }
  },
  methods: {
    scrollToElement(element) {
      const parent = document.querySelector(element).parentElement.parentElement.offsetTop
      const offset = document.querySelector(element).offsetTop + parent
      const headerHeight = this.getHeaderHeight()

      window.scrollTo({
        top: offset - headerHeight,
        behavior: 'smooth'
      })
    },
    getHeaderHeight() {
      const header = document.querySelector('.globalHeader')
      return header.clientHeight + header.offsetTop
    }
  }
}
</script>

<style lang="scss">
.bannerHero {
  /* background: url('~/static/images/bg-placeholder.jpg') center top no-repeat; */
  background-color: $bg;
  background-size: cover;
  min-height: 100vh;

  // animations

  &__header span:nth-child(1),
  &__header span:nth-child(2),
  &__text,
  &__buttonHolder {
    transform: translateY(-30px);
    opacity: 0;
    transition: transform 0.5s, opacity 0.5s;
  }

  &__scrollBtn {
    opacity: 0;
    transition: opacity 0.5s;
    transition-delay: 4s;
  }

  &__container {
    padding-bottom: 120px;
    height: 100%;
  }

  &__header {
    max-width: 411px;
    width: 100%;
    margin-bottom: 32px;

    span {
      &:nth-child(1) {
        color: $white;
        font-weight: 800;
        font-size: 40px;
        line-height: 53px;
        font-family: $karla;
        text-transform: uppercase;
        margin-bottom: 8px;
        transition-delay: 2s;
      }
      &:nth-last-child(1) {
        color: $green;
        font-weight: 900;
        font-size: 80px;
        line-height: 70px;
        font-family: $karla;
        text-transform: uppercase;
        transition-delay: 2.5s;
      }
    }
  }

  &__text {
    line-height: 36px;
    max-width: 500px;
    width: 100%;
    margin-bottom: 32px;
    transition-delay: 3s;
    font-family: $inconsolata;
  }

  &__buttonHolder {
    opacity: 0;
    transition-delay: 3.5s;
  }

  &.is-inview {
    .bannerHero__header span:nth-child(1),
    .bannerHero__header span:nth-child(2),
    .bannerHero__text,
    .bannerHero__buttonHolder {
      transform: translateY(0);
      opacity: 1;
    }

    .bannerHero__scrollBtn {
      opacity: 1;
    }
  }
}

//----------------------------------------//

// 1080
@include breakpoint(xl) {
  .bannerHero {
    &__text {
      font-size: 18px;
    }

    &__header {
      span {
        &:nth-child(1) {
          font-size: 38px;
        }
        &:nth-last-child(1) {
          font-size: 75px;
        }
      }
    }
  }
}

//----------------------------------------//

// 750
@include breakpoint(m) {
  .bannerHero {
    &__header {
      span {
        &:nth-child(1) {
          font-size: 36px;
          margin-bottom: 0;
        }
        &:nth-last-child(1) {
          font-size: 70px;
        }
      }
    }

    &__text {
      max-width: 450px;
    }
  }
}

//----------------------------------------//

// 600
@include breakpoint(s) {
  .bannerHero {
    &__container {
      padding-bottom: 32px;
    }
    &__header {
      max-width: 100%;
      width: 100%;
      margin-bottom: 12px;

      span {
        &:nth-child(1) {
          font-size: 28px;
          line-height: 37px;
          margin-bottom: 0;
        }
        &:nth-last-child(1) {
          font-size: 48px;
          line-height: 70px;
          margin-top: -10px;
        }
      }
    }

    &__button {
      display: none;
    }

    &__text {
      font-size: 16px;
      line-height: 28px;
      margin-bottom: 54px;
    }
  }
}
</style>
