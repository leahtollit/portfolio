<template>
  <section class="globalFooter pos--rel">
    <div class="globalFooter__container container">
      <div class="globalFooter__socials flex justifyC--center alignI--center">
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
  padding: 40px 0;

  &::before {
    content: '';
    position: absolute;
    display: inline-block;
    left: 0;
    top: 0;
    background: $green;
    opacity: 0.4;
    height: 1px;
    width: calc(100% - 88px);
    left: 50%;
    transform: translateX(-50%);
  }

  &__credit {
    font-family: $karla;
    line-height: 30px;
  }

  &__socialItem {
    margin-right: 56px;

    &:nth-last-of-type(1) {
      margin-right: 0px;
    }

    &:hover {
      cursor: pointer;
      .globalFooter__icon {
        fill: $orange;
      }
    }
  }

  &__icon {
    fill: $green;
    transition: fill 0.3s ease;
  }
}
//----------------------------------------//
// 960
@include breakpoint(l) {
  .globalFooter {
    &__flower {
      max-width: 350px;
      height: 350px;
    }
  }
}
//----------------------------------------//
// 750
@include breakpoint(m) {
  .globalFooter {
    &__flower {
      max-width: 300px;
      height: 300px;
    }
  }
}
//----------------------------------------//

// 600
@include breakpoint(s) {
  .globalFooter {
    padding: 24px 0;

    &__flower {
      left: -10%;
      bottom: -56%;
      max-width: 250px;
      height: 250px;
    }

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

//----------------------------------------//
// 500
@include breakpoint(xs) {
  .globalFooter {
    &__flower {
      left: -20%;
      bottom: -102%;
      max-width: 200px;
      height: 200px;
    }
  }
}
</style>
