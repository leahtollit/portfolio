<template>
  <section class="photographyCarousel grid justifyI--center pos--rel z--1">
    <h2 class="photographyCarousel__header fs--56 lh--140 fw--400 ta--center ff--karla o--0 fc--black">
      My passion for <span><a href="https://www.instagram.com/pop.sshots/" target="_blank">photography</a></span>
    </h2>
    <p class="photographyCarousel__text fs--18 lh--180 ta--center o--0 fc--black">
      In my spare time, I love to capture monochrome shots from places I've visited. This was influenced by a university
      project where I created a
      <a class="photographyCarousel__link" href="https://www.youtube.com/watch?v=APoRY0TcldM" target="_blank"
        >transmedia piece</a
      >
      highlighting the importance of colour.
    </p>
    <SliderImages class="photographyCarousel__carousel o--0" />
    <Flower class="photographyCarousel__flower pos--abs" />
  </section>
</template>

<script>
import { inview } from '~/mixins/inview.js'
import Flower from '~/assets/svgs/flower.svg?inline'

export default {
  name: 'PhotographyCarousel',
  mixins: [inview],
  components: {
    Flower
  }
}
</script>

<style lang="scss">
.photographyCarousel {
  padding: 0 0 193px;
  background: $bg;
  overflow: hidden;

  &__flower {
    fill: $greenDark;
    z-index: 0;
    left: -10%;
    bottom: -6%;
    max-width: 500px;
    height: 550px;
  }

  &__header,
  &__text,
  &__carousel,
  &__cta {
    opacity: 0;
    transform: translateY(-30px);
    transition: transform 0.3s ease, opacity 0.5s;
  }

  &__header {
    font-size: 56px;
    font-family: $karla;

    span {
      position: relative;
      color: $green;

      &::after {
        position: absolute;
        content: '';
        width: 100%;
        height: 2px;
        background: $green;
        left: 0;
        bottom: 10px;
        z-index: -1;
        transform: scaleX(1);
        transition: transform 0.3s cubic-bezier(0.25, 0.1, 0.25, 1);
      }

      &:hover::after {
        transform: scaleX(0);
      }
    }
  }

  &__text {
    margin: 16px 0 64px;
    max-width: 550px;
    transition-delay: 0.3s;
    font-family: $inconsolata;
  }

  &__carousel {
    transition-delay: 0.6s;
  }

  &__link {
    position: relative;
    &::after {
      position: absolute;
      content: '';
      width: 100%;
      height: 1px;
      background: $black;
      left: 0;
      bottom: -2px;
      transform: scaleX(1);
      transition: transform 0.3s cubic-bezier(0.25, 0.1, 0.25, 1);
    }

    &:hover::after {
      transform: scaleX(0);
    }
  }

  &__cta.baseBtn {
    margin: 58px 0 0;
    padding: 17px 36px;
    transition-delay: 0.9s;
  }

  &.is-inview {
    .photographyCarousel__header,
    .photographyCarousel__text,
    .photographyCarousel__carousel,
    .photographyCarousel__cta {
      opacity: 1;
      transform: translateY(0);
    }

    .photographyCarousel__text {
      opacity: 0.8;
    }
  }
}

// 960
@include breakpoint(l) {
  .photographyCarousel {
    &__header,
    &__text {
      padding: 0 32px;
    }

    &__header {
      span {
        &::after {
          bottom: 7px;
        }
      }
    }
  }
}

// 600
@include breakpoint(s) {
  .photographyCarousel {
    padding: 95px 0 66px;

    &__header {
      font-size: 32px;
      padding: 0 24px;

      span {
        &::after {
          bottom: 3px;
        }
      }
    }

    &__text {
      font-size: 16px;
      max-width: 100%;
      padding: 0 24px;
    }
  }
}
</style>
