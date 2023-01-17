<template>
  <section id="roadmap" class="ourRoadmap pos--rel">
    <Blob class="ourRoadmap__blob pos--abs" />

    <div class="ourRoadmap__container grid z--1">
      <h2 class="ourRoadmap__header fs--56 fw--400 lh--140 o--0 fc--black ff--karla">My <span>Journey</span></h2>
      <div v-if="slider" class="ourRoadmap__buttons grid grid--flow-c gap--16 16px alignS--start justifyC--start o--0">
        <button
          :class="{ 'ourRoadmap__button--disabled': current === 0 }"
          class="ourRoadmap__button ourRoadmap__button--prev pos--rel z--1"
          @click="slider.prev()">
          <IconPrev />
        </button>
        <button
          :class="{ 'ourRoadmap__button--disabled': current === slider.track.details.slides.length - 1 }"
          class="ourRoadmap__button ourRoadmap__button--next pos--rel z--1"
          @click="slider.next()">
          <IconNext />
        </button>
      </div>
      <div class="ourRoadmap__carousel sliderRoadmap pos--rel">
        <div ref="slider" class="sliderRoadmap__slider keen-slider pos--rel">
          <div
            v-for="(item, i) in slides"
            :key="item + i"
            class="sliderRoadmap__slide keen-slider__slide pos--rel flex justifyC--center"
            :class="{ 'sliderRoadmap__slide--inactive': !item.active }">
            <div class="sliderRoadmap__slideContents pos--rel">
              <h3 class="sliderRoadmap__slideTitle fs--20 fw--400 fc--black">{{ item.title }}</h3>
              <h3 class="sliderRoadmap__slideHeading fs--18 fw--300 fc--black">{{ item.heading }}</h3>

              <ul class="sliderRoadmap__slideList">
                <li v-for="(el, j) in item.items" :key="el + j" class="fs--16 lh--180 fw--400 fc--black">
                  {{ el }}
                </li>
              </ul>
            </div>

            <div class="sliderRoadmap__slideMarker pos--abs xy--center" />
            <div class="sliderRoadmap__slideLine sliderRoadmap__slideLine--prev pos--abs y--center" />
            <div class="sliderRoadmap__slideLine sliderRoadmap__slideLine--next pos--abs y--center" />
          </div>

          <div class="sliderRoadmap__slide keen-slider__slide" />
        </div>
      </div>
    </div>
  </section>
</template>

<script>
// https://keen-slider.io/docs
import 'keen-slider/keen-slider.min.css'
import KeenSlider from 'keen-slider'
import { inview } from '~/mixins/inview.js'
import IconPrev from '~/assets/svgs/interface/prev.svg?inline'
import IconNext from '~/assets/svgs/interface/next.svg?inline'
import Blob from '~/assets/svgs/blob.svg?inline'

export default {
  name: 'OurRoadmap',
  mixins: [inview],
  components: {
    IconPrev,
    IconNext,
    Blob
  },
  data() {
    return {
      current: 0,
      slider: false,
      btns: true,
      slides: [
        {
          title: 'Junior Developer',
          heading: 'Supremo ~ 2021 - present',
          items: [
            'Understanding of Web3',
            'Website sustainment and content updates',
            'Lead client expectations via designer cooperation, intercommunication and brief requirements'
          ],
          active: true
        },
        {
          title: 'Web Dev Placement',
          heading: 'Supremo ~ 2021',
          items: [
            'Low fidelity prototyping',
            'Learnt new frameworks e.g. SASS and Vue.js',
            'Assisted on live client briefs',
            'Develop front-end dev skillset'
          ],
          active: true
        },
        {
          title: 'Digital Media & Comms',
          heading: 'First Class Honours ~ MMU 2021',
          items: [
            ' UX foundations and prototyping',
            'Front-end development',
            'Transmedia asset creation',
            'Theoretical themes in social media'
          ],
          active: true
        },
        {
          title: 'Code First Girls',
          heading: '2019',
          items: [
            '8 week course',
            'learnt aspects of HTML, CSS and JavaScript',
            'Used applications such as Github and Bootstrap',
            'Won a website build competition'
          ],
          active: true
        },
        {
          title: 'Work experience',
          heading: 'Our Name Is Mud ~ 2017',
          items: [
            'Assisted on live projects',
            'Developed Photoshop skills creating mobile responsive design layouts',
            'Basic code understanding using CodeAcademy'
          ],
          active: true
        }
      ]
    }
  },
  mounted() {
    window.addEventListener('resize', () => {
      if (window.innerWidth < 750) {
        if (this.slider) {
          this.slider.destroy()
          this.slider = false
        }
      } else if (!this.slider) {
        this.slider = new KeenSlider(this.$refs.slider, {
          selector: '.sliderRoadmap__slide',
          initial: this.current,
          slideChanged: (s) => {
            this.current = s.track.details.rel
          },
          slides: {
            perView: 4
          },
          breakpoints: {
            '(max-width: 1260px)': {
              slides: {
                perView: 3
              }
            },
            '(max-width: 960px)': {
              slides: {
                perView: 2
              }
            }
          }
        })
      }
    })

    window.dispatchEvent(new Event('resize'))
  },
  destroy() {
    if (this.slider) this.slider.destroy()
  }
}
</script>

<style lang="scss">
.ourRoadmap {
  padding: 82px 0 148px;

  &__container {
    grid-template:
      'header carousel' auto
      'buttons carousel' 1fr / auto 1fr;
  }

  &__blob {
    fill: $green;
    z-index: -1;
    left: -4%;
    bottom: 0;
    max-width: 200px;
    width: 50%;
    transform: scaleX(-1);
  }

  &__header,
  &__buttons,
  &__carousel {
    transform: translateX(-32px);
    transition: opacity 0.6s, transform 0.6s;
  }

  &__header {
    grid-area: header;
    margin: 0 0 0 88px;
    max-width: 260px;
    height: max-content;
    font-size: 56px;
    font-size: $karla;

    span {
      color: $orange;
    }
  }

  &__buttons {
    grid-area: buttons;
    margin: 32px 0 0 88px;
  }

  &__button {
    border: 0;
    border-radius: 50%;
    width: 51px;
    height: 51px;
    background: linear-gradient(45deg, var(--orange), var(--red));
    cursor: pointer;
    transition-delay: 0.6s;

    &::before {
      content: '';
      position: absolute;
      top: 1px;
      right: 1px;
      bottom: 1px;
      left: 1px;
      border-radius: 50%;
      background: var(--bg);
      z-index: -1;
      transition: background 0.3s ease;
    }

    svg {
      fill: $orange;
      transition: fill 0.3s ease;
    }

    &:hover {
      &::before {
        background: $orange;
      }
      svg {
        fill: $white;
      }
    }
  }

  &__carousel {
    grid-area: carousel;
    transform: translateX(32px);
    transition-delay: 0.3s;
  }

  &.is-inview {
    .ourRoadmap__header,
    .ourRoadmap__buttons,
    .ourRoadmap__carousel {
      opacity: 1;
      transform: translateX(0);
    }
  }
}

// 1400
@include breakpoint(xxxl) {
  .ourRoadmap {
    &__header {
      margin: 0 0 0 40px;
    }

    &__buttons {
      margin: 32px 0 0 40px;
    }
  }
}

// 750
@include breakpoint(m) {
  .ourRoadmap {
    padding: 80px 0 96px;

    &__container {
      grid-template:
        'header'
        'carousel';
      justify-items: center;
    }

    &__header {
      margin: 0 0 32px;
      font-size: 32px;
      text-align: center;
    }
  }
}

.sliderRoadmap {
  &__slider {
    overflow: hidden;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    -webkit-touch-callout: none;
    -khtml-user-select: none;
    touch-action: pan-y;
    -webkit-tap-highlight-color: transparent;
    max-width: calc(100vw - 348px);
    padding-left: 20px;
  }

  &__slide {
    --direction: 90deg;
    height: 896px;
    overflow: visible !important;

    &:not(.sliderRoadmap__slide--inactive) + .sliderRoadmap__slide--inactive .sliderRoadmap__slideLine--prev {
      background: linear-gradient(45deg, $orange, $red);
    }

    &--inactive {
      .sliderRoadmap__slideContents {
        opacity: 0.3;
      }

      .sliderRoadmap__slideMarker {
        background: #112240;

        &::before {
          background: #112240;
        }
      }

      & + .sliderRoadmap__slide--inactive .sliderRoadmap__slideLine--prev {
        background: #112240;
      }

      & + .sliderRoadmap__slide:not(.sliderRoadmap__slide--inactive) .sliderRoadmap__slideLine--prev {
        background: linear-gradient(var(--direction), $red, $orange);
      }

      &:first-child {
        .sliderRoadmap__slideLine--prev {
          background: linear-gradient(var(--direction), transparent, var(--blue)) !important;
        }
      }

      &:nth-last-child(2) {
        .sliderRoadmap__slideLine--next {
          background: linear-gradient(var(--direction), #112240, transparent) !important;
        }
      }
    }

    &:first-child {
      .sliderRoadmap__slideLine--prev {
        left: 0;
        width: 50%;
        background: linear-gradient(var(--direction), transparent, var(--red));
      }
    }

    &:nth-last-child(2) {
      .sliderRoadmap__slideLine--next {
        width: 50%;
        background: linear-gradient(var(--direction), var(--orange), transparent);
        opacity: 1;
      }
    }

    &:nth-child(odd) {
      .sliderRoadmap__slideContents {
        margin-top: auto;
      }

      .sliderRoadmap__slideMarker:before {
        top: auto;
        bottom: -93px;
      }
    }
  }
  &__slideList {
    font-family: $inconsolata;
  }
  &__slideContents {
    padding: 46px 0;
    width: 250px;
    height: 340px;

    &::before,
    &::after {
      content: '';
      position: absolute;
    }

    &::before {
      top: 0;
      left: -40px;
      width: calc(100% + 80px);
      height: 100%;
      background: linear-gradient(45deg, var(--red), var(--red));
      z-index: -2;
    }

    &::after {
      top: 1px;
      left: -39px;
      width: calc(100% + 78px);
      height: calc(100% - 2px);
      background: var(--bg);
      z-index: -1;
    }
  }

  &__slideTitle {
    margin-bottom: 8px;
    font-family: $karla;
  }

  &__slideHeading {
    margin-bottom: 16px;
    font-family: $karla;
  }

  &__slideMarker {
    border-radius: 50%;
    width: 31px;
    height: 31px;
    background: var(--orange);

    &::before {
      content: '';
      position: absolute;
      top: -93px;
      left: 50%;
      width: 1px;
      height: 108px;
      background: var(--orange);
    }
  }

  &__slideLine {
    width: 50%;
    height: 1px;
    background: var(--orange);
    z-index: -1;

    &--prev {
      left: -50%;
      width: 100%;
    }

    &--next {
      right: 0;
      opacity: 0;
    }
  }

  //
  &__dots {
    margin: 10px 0 20px;
  }

  &__dot {
    margin: 0 4px;
    border: none;
    border-radius: 50%;
    width: 10px;
    height: 10px;
    background: rgba(var(--rgb-black), 0.3);
    cursor: pointer;

    &--active {
      background: var(--black);
    }
  }

  //
  &__btn {
    cursor: pointer;

    &--disabled {
      opacity: 0.5;
      pointer-events: none;
    }
  }
}

// 1400
@include breakpoint(sl) {
  .sliderRoadmap {
    &__slider {
      max-width: calc(100vw - 300px);
    }

    &__slideContents {
      width: 225px;

      &:before {
        left: -28px;
        width: calc(100% + 56px);
      }

      &:after {
        left: -27px;
        width: calc(100% + 54px);
      }
    }

    &__slideList li {
      font-size: 14px;
    }
  }
}

// 960
@include breakpoint(l) {
  .sliderRoadmap {
    &__slideContents {
      padding: 24px 0;
      // width: 150px;

      &::before {
        left: -24px;
        width: calc(100% + 48px);
      }

      &::after {
        left: -23px;
        width: calc(100% + 46px);
      }

      // & li {
      // 	font-size: 14px;
      // }
    }

    &__slideTitle {
      font-size: 18px;
    }
  }
}

// 750
@include breakpoint(m) {
  .ourRoadmap {
    &__blob {
      left: unset;
      right: -10%;
      bottom: -10%;
      height: 150px;
    }
  }
  .sliderRoadmap {
    padding: 0 0 32px;
    width: 100%;

    &::before {
      display: none;
    }

    &__slider {
      display: grid !important;
      gap: 16px;
      overflow: visible !important;
      max-width: 100vw;
      padding: 0;
    }

    &__slide {
      --direction: 180deg;
      margin: 0;
      height: max-content;
    }

    &__slideContents {
      padding: 24px;
      width: 100%;
      height: max-content;

      &::before {
        left: 0;
        width: 100%;
      }

      &::after {
        top: 2px;
        left: 2px;
        width: calc(100% - 4px);
        height: calc(100% - 4px);
      }
    }

    &__slideMarker {
      left: -13px;
      width: 14px;
      height: 14px;

      &::before {
        top: 6px !important;
        bottom: auto !important;
        width: 14px;
        height: 2px;
      }
    }

    &__slideLine {
      width: 1px;
      height: 50%;

      &--prev {
        top: 32px;
        left: -14px !important;
        height: calc(100% + 32px);
        width: 2px !important;
      }

      &--next {
        right: auto;
        top: calc(100% + 32px);
        left: -14px !important;
        height: calc(100% - 32px);
        width: 2px !important;
      }
    }
  }
}

// 600
@include breakpoint(s) {
  .ourRoadmap {
    &__blob {
      right: -15%;
    }
  }
}

// 500
@include breakpoint(xs) {
  .ourRoadmap {
    &__blob {
      bottom: -5%;
      right: -20%;
    }
  }
}
</style>
