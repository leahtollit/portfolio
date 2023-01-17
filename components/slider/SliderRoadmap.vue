<template>
  <div class="sliderRoadmap pos--rel">
    <div ref="slider" class="sliderRoadmap__slider keen-slider pos--rel">
      <div
        v-for="(item, i) in slides"
        :key="item + i"
        class="sliderRoadmap__slide keen-slider__slide pos--rel flex justifyC--center"
        :class="{ 'sliderRoadmap__slide--inactive': !item.active }">
        <div class="sliderRoadmap__slideContents pos--rel">
          <h3 class="sliderRoadmap__slideTitle fs--24 fw--400 fc--orange">{{ item.title }}</h3>
          <ul class="sliderRoadmap__slideList">
            <li v-for="(el, j) in item.items" :key="el + j" class="fs--14 lh--180 fw--400">
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

    <div v-if="slider" class="sliderRoadmap__dots flex justifyC--center">
      <button
        v-for="(el, i) in slider.track.details.slides.length"
        :key="el + i"
        :class="{ 'sliderRoadmap__dot--active': current === i }"
        class="sliderRoadmap__dot buttonReset"
        @click="slider.moveToIdx(i)" />
    </div>

    <div v-if="btns" class="sliderRoadmap__btns flex justifyC--center">
      <button
        :class="{ 'sliderRoadmap__btn--disabled': current === 0 }"
        class="sliderRoadmap__btn sliderRoadmap__btn--prev"
        @click="slider.prev()">
        Previous
      </button>

      <button
        :class="{ 'sliderRoadmap__btn--disabled': current === slider.track.details.slides.length - 1 }"
        class="sliderRoadmap__btn sliderRoadmap__btn--next"
        @click="slider.next()">
        Next
      </button>
    </div>
  </div>
</template>

<script>
// https://keen-slider.io/docs
import 'keen-slider/keen-slider.min.css'
import KeenSlider from 'keen-slider'

export default {
  name: 'SliderRoadmap',
  data() {
    return {
      current: 0,
      slider: false,
      btns: false,
      slides: [
        {
          title: 'Q1 2022',
          items: [
            'Seed/Private Sale',
            'Team Expansion',
            'Community Launch',
            'Media & Marketing',
            'Full Development Team Onboarded'
          ],
          active: true
        },
        {
          title: 'Q2 2022',
          items: ['Close Seed Round', 'Continue Alpha', 'Marketing GTM Team', 'Expand Marketplace Development'],
          active: true
        },
        {
          title: 'Q3 2022',
          items: [
            'Private Round & Partners',
            'Continued Alpha Development',
            'Virtual Worlds Consumer & Business',
            'Token creation, mint, audit'
          ],
          active: true
        },
        {
          title: 'Q4 2022',
          items: [
            'Closed Alpha Metaverse Launch',
            'Game Asset NFT Sales',
            'Exchange Listing',
            'Staking & Rewards',
            'NFT Access Pools'
          ],
          active: true
        },
        {
          title: 'Q1 2023',
          items: [
            'New Game Release',
            'Additional Chains - Polygon+',
            'Multiplayer Enhancements',
            'Alpha Downloadable Client'
          ],
          active: false
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
.sliderRoadmap {
  background: $bg;

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
      background: linear-gradient(var(--direction), var(--orange), var(--bg));
    }

    &--inactive {
      .sliderRoadmap__slideContents {
        opacity: 0.3;
      }

      .sliderRoadmap__slideMarker {
        background: #2d316f;

        &::before {
          background: #2d316f;
        }
      }

      & + .sliderRoadmap__slide--inactive .sliderRoadmap__slideLine--prev {
        background: #2d316f;
      }

      & + .sliderRoadmap__slide:not(.sliderRoadmap__slide--inactive) .sliderRoadmap__slideLine--prev {
        background: linear-gradient(var(--direction), var(--pink), var(--blue));
      }

      &:first-child {
        .sliderRoadmap__slideLine--prev {
          background: linear-gradient(var(--direction), transparent, var(--blue)) !important;
        }
      }

      &:nth-last-child(2) {
        .sliderRoadmap__slideLine--next {
          background: linear-gradient(var(--direction), #2d316f, transparent) !important;
        }
      }
    }

    &:first-child {
      .sliderRoadmap__slideLine--prev {
        left: 0;
        width: 50%;
        background: linear-gradient(var(--direction), transparent, var(--orange));
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
      background: linear-gradient(45deg, var(--orange), var(--red));
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
    margin-bottom: 16px;
    color: var(--orange);
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

// 1500
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
  .sliderRoadmap {
    padding: 0 32px;
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
</style>
