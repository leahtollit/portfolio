<template>
  <main class="theContent">
    <BannerHero id="intro" />
    <PhotographyCarousel id="hobbies" />
    <AwardsGrid id="awards" />
    <OurRoadmap id="experience" />
  </main>
</template>

<script>
import { transitions } from '~/mixins/transitions'

export default {
  name: 'PageHome',
  mixins: [
    transitions
    // locomotive
    // builder
  ]
}
</script>
