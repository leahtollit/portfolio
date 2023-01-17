<template>
  <div class="sliderBase pos--rel">
    <div ref="slider" class="sliderBase__slider keen-slider flex pos--rel">
      <div v-for="(el, i) in 6" :key="el + i" class="sliderBase__slide keen-slider__slide pos--rel grid placeI--center">
        {{ i + 1 }}
      </div>
    </div>

    <div v-if="slider" class="sliderBase__dots flex justifyC--center">
      <button
        v-for="(el, i) in slider.track.details.slides.length"
        :key="el + i"
        :class="{ 'sliderBase__dot--active': current === i }"
        class="sliderBase__dot buttonReset"
        @click="slider.moveToIdx(i)" />
    </div>

    <div class="sliderBase__btns flex justifyC--center">
      <button
        :class="{ 'sliderBase__btn--disabled': current === 0 }"
        class="sliderBase__btn sliderBase__btn--prev"
        @click="slider.prev()">
        Previous
      </button>

      <button
        v-if="slider"
        :class="{ 'sliderBase__btn--disabled': current === slider.track.details.slides.length - 1 }"
        class="sliderBase__btn sliderBase__btn--next"
        @click="slider.next()">
        Next
      </button>
    </div>
  </div>
</template>

<script>
// https://keen-slider.io/docs
import KeenSlider from 'keen-slider'
import 'keen-slider/keen-slider.min.css'

export default {
  name: 'SliderBase',
  data() {
    return {
      current: 0,
      slider: null
    }
  },
  mounted() {
    this.slider = new KeenSlider(this.$refs.slider, {
      selector: '.sliderBase__slide',
      initial: this.current,
      slideChanged: (s) => {
        this.current = s.track.details.rel
      }
    })
  },
  destroy() {
    if (this.slider) this.slider.destroy()
  }
}
</script>

<style lang="scss">
.sliderBase {
  //
  &__slider {
    flex-wrap: nowrap;
    align-content: flex-start;
    overflow: hidden;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    -webkit-touch-callout: none;
    -khtml-user-select: none;
    touch-action: pan-y;
    -webkit-tap-highlight-color: transparent;
    width: 100%;
  }

  &__slide {
    overflow: hidden;
    width: 100%;
    background: var(--black);
    font-size: 50px;
    color: var(--white);
    height: 200px;
  }

  //
  &__dots {
    margin: 10px 0 20px;
  }

  &__dot {
    border: none;
    width: 10px;
    height: 10px;
    background: rgba(var(--rgb-black), 0.3);
    border-radius: 50%;
    margin: 0 4px;
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
</style>
