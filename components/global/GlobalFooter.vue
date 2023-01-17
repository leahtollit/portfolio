<template>
  <section class="globalFooter pos--rel">
    <div class="globalFooter__container container">
      <div class="globalFooter__socialsHolder flex justifyC--between alignI--center">
        <NuxtLink to="/" class="globalFooter__logoHolder pos--rel">
          <!-- <GlobalLogo class="globalFooter__logo pos--abs" /> -->
        </NuxtLink>

        <div class="globalFooter__socials flex justifyC--between alignI--center">
          <a
            href="https://twitter.com/_leahtollit"
            class="globalFooter__socialItem fc--white ff--karla fs--18 fw--300"
            target="_blank">
            <IconTwitter class="globalFooter__icon globalFooter__icon--twitter" />
          </a>
          <a
            ref="mailto:leahtollit@gmail.com"
            class="globalFooter__socialItem fc--white ff--karla fs--18 fw--300"
            target="_blank">
            <IconEmail class="globalFooter__icon globalFooter__icon--email" />
          </a>
          <a
            href="https://www.linkedin.com/in/leah-tollit-7aaa78172/"
            class="globalFooter__socialItem fc--white ff--karla fs--18 fw--300"
            target="_blank">
            <IconLinkedin class="globalFooter__icon globalFooter__icon--linkedin" />
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import IconEmail from '~/assets/svgs/socials/email.svg?inline'
import IconTwitter from '~/assets/svgs/socials/twitter.svg?inline'
import IconLinkedin from '~/assets/svgs/socials/linkedin.svg?inline'

export default {
  name: 'GlobalFooter',
  components: {
    IconLinkedin,
    IconTwitter,
    IconEmail
  }
}
</script>

<style lang="scss">
.globalFooter {
  padding: 58px 0 69px;
  /* margin: 40px 0 0; */
  background: $bg;

  &::before {
    content: '';
    position: absolute;
    display: inline-block;
    left: 0;
    top: 0;
    background: rgba(255, 255, 255, 0.6);
    opacity: 0.4;
    height: 1px;
    width: 100%;
  }

  &__credit {
    font-family: $karla;
    line-height: 30px;
  }

  &__logoHolder {
    width: 219px;
    height: 49px;
    display: inline-block;
  }

  &__socialItem {
    margin-right: 56px;

    &:nth-last-of-type(1) {
      margin-right: 0px;
    }

    &:hover {
      .globalFooter__icon {
        fill: $green;
      }
    }
  }

  &__icon {
    fill: $white;
    transition: fill 0.3s ease;
  }
}

//----------------------------------------//

// 600
@include breakpoint(s) {
  .globalFooter {
    padding: 24px 0;

    &__logoHolder {
      margin-bottom: 20px;
      width: 143px;
      height: 32px;
    }

    &__socialsHolder {
      flex-direction: column;
      align-items: flex-start;
    }

    &__socialItem {
      margin-right: 22px;

      &:nth-last-of-type(1) {
        margin-right: 0px;
      }
    }
  }
}
</style>
