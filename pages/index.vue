<template>
  <main class="theContent">
    <BannerHero id="intro" />
    <MyWork id="work" />
    <OurRoadmap id="experience" />
    <AwardsGrid id="certifications" />
    <PhotographyCarousel id="hobbies" />
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
