<template>
  <div class="sliderImages pos--rel">
    <div ref="slider" class="sliderImages__slider keen-slider pos--rel">
      <div v-for="(slide, i) in slides" :key="slide + i" class="sliderImages__slide keen-slider__slide">
        <div class="sliderImages__wrap grid alignI--end pos--rel">
          <img class="sliderImages__image" :src="`/images/photography/${slide.image}.jpeg`" />
          <p class="sliderImages__text fs--18 lh--180 o--0 ff--karla fc--white pos--rel z--1">{{ slide.text }}</p>
        </div>
      </div>
    </div>

    <div v-if="dots" class="sliderImages__dots flex justifyC--center">
      <button
        v-for="(el, i) in slider.track.details.slides.length"
        :key="el + i"
        :class="{ 'sliderImages__dot--active': current === i }"
        class="sliderImages__dot buttonReset"
        @click="slider.moveToIdx(i)" />
    </div>

    <button
      class="sliderImages__button sliderImages__button--prev pos--abs z--2 grid placeI--center"
      @click="slider.prev()">
      <IconPrev />
    </button>

    <button
      class="sliderImages__button sliderImages__button--next pos--abs z--2 grid placeI--center"
      @click="slider.next()">
      <IconNext />
    </button>
  </div>
</template>

<script>
// https://keen-slider.io/docs
import 'keen-slider/keen-slider.min.css'
import KeenSlider from 'keen-slider'
import IconPrev from '~/assets/svgs/interface/prev.svg?inline'
import IconNext from '~/assets/svgs/interface/next.svg?inline'

export default {
  name: 'sliderImages',
  components: {
    IconPrev,
    IconNext
  },
  data() {
    return {
      current: 0,
      slider: false,
      dots: false,
      slides: [
        {
          image: 'derwent-lake',
          text: 'Derwent Lake, Lake District'
        },
        {
          image: 'edinburgh-streets',
          text: 'The Royal Mile, Edinburgh'
        },
        {
          image: 'edinburgh',
          text: 'National Museum of Scotland, Edinburgh'
        },
        {
          image: 'israel',
          text: 'Tel Aviv, Israel'
        },
        {
          image: 'italy-2',
          text: 'Verona, Italy'
        },
        {
          image: 'italy',
          text: 'Lake Garda, Italy'
        },
        {
          image: 'media-city',
          text: 'Media City, Salford'
        },
        {
          image: 'york',
          text: 'York Cathedral, York'
        }
      ]
    }
  },
  mounted() {
    this.slider = new KeenSlider(this.$refs.slider, {
      initial: this.current,
      slideChanged: (s) => {
        this.current = s.track.details.rel
      },
      slides: {
        perView: 1,
        spacing: 0
      },
      loop: true,
      breakpoints: {
        '(min-width: 750px)': {
          slides: {
            perView: 2,
            spacing: 32
          }
        },
        '(min-width: 960px)': {
          slides: {
            perView: 3,
            spacing: 48
          }
        },
        '(min-width: 1200px)': {
          slides: {
            perView: 4,
            spacing: 48
          }
        },
        '(min-width: 1400px)': {
          slides: {
            perView: 4,
            spacing: 60
          }
        }
      }
    })
  },
  destroy() {
    if (this.slider) this.slider.destroy()
  }
}
</script>

<style lang="scss">
.sliderImages {
  width: 100%;

  &::before,
  &::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 300px;
    height: 100%;
    background: linear-gradient(90deg, var(--blueDarker), transparent);
    z-index: 1;
    pointer-events: none;
  }

  &__text {
    font-family: $inconsolata;
  }

  &::after {
    right: 0;
    left: auto;
    background: linear-gradient(90deg, transparent, var(--blueDarker));
  }

  &__slider {
    max-width: 100vw;
    -webkit-touch-callout: none;
    -webkit-tap-highlight-color: transparent;
    -webkit-user-select: none;
    user-select: none;
    touch-action: pan-y;
    overflow: hidden;
  }

  &__slide {
    &:hover {
      cursor: pointer;
      .sliderImages__logo {
        opacity: 0;
      }

      .sliderImages__text {
        opacity: 0.8;
      }
    }
  }

  &__image {
    width: 100%;
    aspect-ratio: 1 / 1;
  }

  &__image,
  &__logo,
  &__text {
    grid-area: 1 / -1;
  }

  &__logo,
  &__text {
    padding: 20px;
    transition: opacity 0.3s;

    &::before {
      content: '';
      position: absolute;
      left: 0;
      bottom: 0;
      width: 100%;
      height: 150%;
      background: linear-gradient(transparent, black);
      z-index: -1;
    }
  }

  &__logo img {
    width: 50%;
  }

  &__button {
    bottom: 50%;
    border: 1px solid rgba(white, 0.5);
    border-radius: 50%;
    width: 51px;
    height: 51px;
    background: none;
    cursor: pointer;
    transform: translateY(50%);
    transition: border 0.3s, background 0.3s;

    &:hover {
      border-color: white;
      background: rgba(white, 0.125);
    }

    &--prev {
      left: 72px;
    }

    &--next {
      right: 72px;
    }
  }
}

// 1400
@include breakpoint(sl) {
  .sliderImages {
    &__text {
      font-size: 14px;
    }
  }
}

// 960
@include breakpoint(l) {
  .sliderImages {
    &::before,
    &::after {
      width: 50px;
    }

    &__slide {
      padding: 0 48px;
    }

    &__button {
      &--prev {
        left: 32px;
      }

      &--next {
        right: 32px;
      }
    }
  }
}

// 750
@include breakpoint(m) {
  .sliderImages {
    &::before,
    &::after {
      display: none;
    }

    &__button {
      &--prev {
        left: 16px;
      }

      &--next {
        right: 16px;
      }
    }
  }
}
</style>
