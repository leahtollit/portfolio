<template>
  <section class="awardGrid pos--rel z--2">
    <div class="awardGrid__container container flex pos--rel flex--dir-c z--2">
      <div class="awardGrid__headerHolder flex flex--dir-c">
        <p class="awardGrid__heading ff--karla fw--600 fs--24 fc--white pos--rel">Certifications</p>
        <p class="awardGrid__header ff--inconsolata fs--35 fw--900 fc--white">
          I like to continually develop my understanding of my field, utilising online platforms such as LinkedIn
          Learning and Udemy to further enhance my skillset.
        </p>
      </div>
      <div class="awardGrid__holder">
        <div class="awardGrid__items">
          <div v-for="(el, i) in items" :key="el + i" class="awardGrid__itemHolder">
            <div class="awardGrid__body flex alignI--center">
              <div class="awardGrid__imgHolder pos--rel">
                <img class="awardGrid__img pos--abs" :src="el.image" alt="" />
              </div>
              <div class="awardGrid__copyHolder flex flex--dir-c">
                <p class="awardGrid__title ff--archivo fw--600 fs--24 fc--white pos--rel">{{ el.title }}</p>
                <p class="awardGrid__text ff--archivo fw--400 fs--16 fc--white pos--rel o--8">
                  {{ el.text }}
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { inview } from '~/mixins/inview.js'

export default {
  name: 'awardGrid',
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
  data() {
    return {
      items: [
        {
          image: '/images/socials/linkedin.png',
          title: 'SEO Foundations',
          text: 'Strategies behind great SEO including keyword planning, link building and SEO for ecommerce, and mobile audiences.'
        },
        {
          image: '/images/socials/linkedin.png',
          title: 'UX Foundations Prototyping',
          text: 'Learnt the basics of prototyping. Understood how to build prototypes which allow you me to test and validate my UX designs.'
        },
        {
          image: '/images/socials/linkedin.png',
          title: 'User Experience for Web Design',
          text: ' Mastered simple interaction design principles which allowed me to apply them to websites to make them behave in the way that users expect.'
        },
        {
          image: '/images/socials/udemy.png',
          title: 'Advanced CSS and Sass',
          text: 'Advanced CSS and Sass - flexbox, CSS Grid, responsive design, animations'
        },
        {
          image: '/images/socials/icdl.png',
          title: 'ICDL',
          text: 'Helped develop and enhance my digital skills pre-higher education'
        }
      ]
    }
  }
}
</script>

<style lang="scss">
.awardGrid {
  padding: 82px 0 148px;
  /* overflow: hidden; */

  &__heading,
  &__header {
    transform: translateY(-30px);
    opacity: 0;
    transition: transform 0.5s, opacity 0.5s;
  }

  &__heading {
    font-size: 24px;
    font-family: $karla;
    margin-bottom: 46px;
    padding-left: 56px;
    line-height: 26px;
    display: inline-block;
    transition-delay: 0.3s;

    &::before {
      content: '';
      position: absolute;
      display: inline-block;
      left: 0;
      top: 50%;
      background: $white;
      height: 3px;
      width: 29px;
    }
  }

  &__headerHolder {
    margin-bottom: 106px;
  }

  &__header {
    font-weight: 400;
    max-width: 703px;
    width: 100%;
    line-height: 46px;
    font-size: 28px;
    transition-delay: 0.6s;
    font-family: $inconsolata;
  }

  &__holder {
    width: 100%;
    max-width: 1200px;
    margin: 0 auto 0;
  }

  &__body {
    flex-direction: row;
    position: relative;
    top: 50%;
    width: 478px;
    height: 100%;
  }

  &__itemHolder {
    position: relative;
    display: flex;
    width: 100%;
    margin-bottom: -24px;

    &:nth-last-of-type(1) {
      margin-bottom: 0;
    }

    &:nth-child(1) {
      transition-delay: 0.3s;
    }

    &:nth-child(2) {
      transition-delay: 0.6s;
    }

    &:nth-child(3) {
      transition-delay: 0.9s;
    }

    &:nth-child(4) {
      transition-delay: 1.2s;
    }

    &:nth-child(5) {
      transition-delay: 1.5s;
    }

    &:nth-child(2n) {
      justify-content: flex-end;
      transform: translateX(30px);
    }

    transform: translateX(-30px);
    opacity: 0;
    transition: transform 0.5s, opacity 0.5s;
  }

  &__imgHolder {
    width: 90px;
    height: 90px;
    margin-right: 21px;
    border-radius: 50%;
  }

  &__img {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }

  &__title {
    margin-bottom: 20px;
    line-height: 26px;
    font-family: $karla;
  }

  &__copyHolder {
    width: calc(100% - 180px);
  }

  &__text {
    line-height: 30px;
    font-family: $inconsolata;
  }

  &__bg {
    bottom: -49%;
    width: 100%;

    &--mobile {
      display: none;
    }
  }

  &__mobileBg {
    width: 100%;
    height: 100%;
    background: $blue;
    left: 0;
    bottom: 0;
    display: none;
  }

  &.is-inview {
    .awardGrid__header,
    .awardGrid__heading {
      transform: translateY(0);
      opacity: 1;
    }

    .awardGrid__itemHolder {
      transform: translateX(0);
      opacity: 1;
    }
  }
}

//----------------------------------------//
// 1600
@include breakpoint(ssl) {
  .awardGrid {
    &__bg {
      bottom: -32%;
    }
  }
}

//----------------------------------------//
// 1500
@include breakpoint(sl) {
  .awardGrid {
    &__bg {
      bottom: -22%;
    }
  }
}
//----------------------------------------//
// 1200
@include breakpoint(xxl) {
  .awardGrid {
    /* &__imgHolder {
      width: 140px;
      height: 140px;
    } */

    &__copyHolder {
      width: calc(100% - 161px);
    }
  }
}

//----------------------------------------//

// 1080
@include breakpoint(xl) {
  .awardGrid {
    &__title {
      margin-bottom: 10px;
      font-size: 22px;
    }

    &__body {
      width: calc(50% - 63px);
      margin-right: 63px;
    }

    &__header {
      font-size: 32px;
    }
  }
}

//----------------------------------------//

// 960
@include breakpoint(l) {
  .awardGrid {
    &__body {
      width: calc(50% - 31px);
      margin-right: 31px;
    }

    &__bg {
      display: none;

      &--mobile {
        display: inline-block;
        top: -26%;
        width: 100%;
      }
    }
  }
}

//----------------------------------------//

// 750
@include breakpoint(m) {
  .awardGrid {
    padding: 64px 0 80px;

    &__itemHolder {
      justify-content: space-between;
    }

    &__headingHolder {
      margin-bottom: 24px;
    }
    &__heading {
      margin-bottom: 32px;
      color: $white;

      &::before {
        background: $white;
      }
    }

    &__header {
      font-size: 24px;
      line-height: 32px;
      color: $white;
    }

    &__headerHolder {
      margin-bottom: 24px;
    }

    &__body {
      margin-bottom: 32px;
      width: 100%;
      max-width: 100%;
      height: 100%;
      margin-right: 0;
      flex-direction: column;
      align-items: center;
      justify-content: center;

      &:nth-last-of-type(0) {
        margin-bottom: 0;
      }
    }

    &__itemHolder {
      margin-bottom: 0;
    }

    &__imgHolder {
      /* width: 128px;
      height: 128px; */
      margin-right: 0;
      margin-bottom: 12px;
    }

    &__copyHolder {
      max-width: 400px;
      width: 100%;
    }

    &__title {
      margin-bottom: 8px;
      font-size: 18px;
      line-height: 20px;
    }

    &__text {
      line-height: 26px;
    }

    &__text,
    &__title {
      text-align: center;
    }

    &__title {
      margin-bottom: 10px;
      font-size: 20px;
    }
  }
}

//----------------------------------------//

// 600
@include breakpoint(s) {
  .awardGrid {
    &__copyHolder {
      max-width: 327px;
    }
  }
}

//----------------------------------------//

// 400
@include breakpoint(xs) {
  .awardGrid {
    &__copyHolder {
      max-width: 100%;
    }

    &__bg {
      &--mobile {
        top: -12%;
      }
    }
  }
}
</style>
