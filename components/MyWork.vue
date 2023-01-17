<template>
  <section id="myWork" :class="margin" class="myWork pos--rel" data-scroll-section data-scroll-persistent="yes">
    <h2 class="myWork__header">My <span>Work</span></h2>

    <div class="myWork__clients">
      <div v-for="(client, i) in work" :key="client + i" class="myWork__client pos--rel">
        <img class="myWork__client-image pos--abs" :src="`/images/${client.image}.jpg`" alt="" />

        <div class="myWork__client-overlay pos--abs">
          <a :href="client.link" target="_blank" class="myWork__link">
            <h3 class="myWork__text">{{ client.text }}</h3>
            <p class="myWork__role">{{ client.role }}</p>
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { inview } from '~/mixins/inview.js'

export default {
  name: 'MyWork',
  mixins: [inview],
  data() {
    return {
      work: [
        {
          image: 'medicys',
          link: 'https://medicysltd.co.uk/',
          text: 'Medicys',
          role: 'Lead development'
        },
        {
          image: 'edinburgh-streets',
          link: 'https://campfire.co.uk/',
          text: 'Campfire',
          role: 'Lead development'
        },
        {
          image: 'metaversus',
          link: 'https://metaversus.world/',
          text: 'Metaversus',
          role: 'Development'
        },
        {
          image: 'derwent-lake',
          link: 'derwent-lake',
          text: 'KO Adobe MAX',
          role: 'Development'
        },
        {
          image: 'branding-science',
          link: 'https://branding-science.com/',
          text: 'Branding Science',
          role: 'Website sustainment and content updates'
        },
        {
          image: 'mmh',
          link: 'https://www.supremo.co.uk/manchesters-most-haunted/',
          text: 'Manchesters Most Haunted',
          role: 'Website re-skin and content updates'
        },
        {
          image: 'cocktail-trading-co',
          link: 'https://thecocktailtradingco.com/',
          text: 'Cocktail Trading Co',
          role: 'Development (placement)'
        },
        {
          image: 'blockbucket',
          link: 'https://blockbucket.io/',
          text: 'Block Bucket',
          role: 'SEO and development'
        }
      ]
    }
  }
}
</script>

<style lang="scss">
.myWork {
  text-align: center;
  padding-top: 82px;

  &__header,
  &__subheader,
  &__client {
    opacity: 0;
    transform: translateY(-30px);
    transition: transform 0.3s ease, opacity 0.5s;
  }
  &__header {
    font-size: 56px;
    margin: 0 0 44px;
    font-family: $karla;

    span {
      color: $red;
      pointer-events: none;
    }
  }

  &__subheader {
    font-size: 19px;
    line-height: 1.8;
    max-width: 700px;
    margin: 0 auto 100px;
    font-size: $inconsolata;
  }

  &__clients {
    display: flex;
    flex-wrap: wrap;
  }

  &__link {
    &:hover {
      cursor: pointer;
    }
  }

  &__client {
    width: 25%;
    background: $bg;

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

    &:nth-child(6) {
      transition-delay: 1.8s;
    }

    &:nth-child(7) {
      transition-delay: 2.1s;
    }

    &:nth-child(8) {
      transition-delay: 2.4s;
    }

    &:after {
      content: '';
      display: block;
      padding-bottom: 100%;
    }

    &:hover {
      .myWork__client-overlay {
        opacity: 1;
        pointer-events: all;
      }
    }

    &-image {
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    &-overlay {
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      justify-content: flex-end;
      padding: 25px;
      background: $red;
      color: white;
      text-align: left;
      pointer-events: none;
      opacity: 0;
      transition: opacity 0.3s;

      h3 {
        font-size: 23px;
        margin: 0 0 7px;
        font-family: $karla;
      }

      p {
        font-size: 19px;
        font-weight: 300;
        margin: 0 0 10px;
        font-family: $inconsolata;
      }
    }
  }

  &_social-link {
    svg {
      width: 26px;
      height: 26px;
    }
  }

  &.is-inview {
    .myWork__header,
    .myWork__subheader,
    .myWork__client {
      transform: translateY(0);
      opacity: 1;
    }
  }
}

/*------------------------------------------*/

// < 1600px
@include breakpoint(ssl) {
}

/*------------------------------------------*/

// < 1400px
@include breakpoint(xxxl) {
}

/*------------------------------------------*/

// < 1200px
@include breakpoint(xxl) {
  .myWork {
    h2 {
      font-size: 36px;
      margin: 0 0 16px;
    }

    &__subheader {
      font-size: 14px;
      max-width: 564px;
      margin-bottom: 75px;
      padding: 0 16px;
    }

    &__client-overlay {
      h3 {
        font-size: 17px;
      }

      p {
        font-size: 14px;
      }
    }
  }
}

/*------------------------------------------*/

// < 960px
@include breakpoint(l) {
  .myWork {
    &__client {
      width: 33.33%;

      &-overlay {
        padding: 20px;
      }
    }
  }
}

/*------------------------------------------*/

// < 750px
@include breakpoint(m) {
}

/*------------------------------------------*/

// < 500px
@include breakpoint(xs) {
  .myWork {
    &__client {
      width: 50%;

      &-overlay {
        padding: 16px;
      }
    }
  }
}

/*------------------------------------------*/
</style>
