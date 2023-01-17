<template>
  <NuxtLink v-if="type === 'internal'" :to="to" class="baseBtn pos--rel grid placeI--center ta--center lh--140">
    <p class="baseBtn__label fc--blue fs--16 ff--karla fw--500"><slot /></p>
  </NuxtLink>

  <button v-else :to="to" class="baseBtn pos--rel align--center" @click="click">
    <p class="baseBtn__label fc--blue fs--16 ff--karla fw--400"><slot /></p>
  </button>
</template>

<script>
export default {
  name: 'BaseBtn',
  props: {
    click: {
      type: Function,
      default: () => {}
    },
    type: {
      type: String,
      default: ''
    },
    to: {
      type: String,
      default: ''
    }
  }
}
</script>

<style lang="scss">
.baseBtn {
  // border: 1px solid white;
  padding: 12px 32px;
  border-radius: 100px;
  background: transparent;
  border: 1px solid $red;
  transition: background 0.3s ease, border-color 0.3s ease, transform 0.3s ease;

  &__label {
    transition: color 0.3s ease;
    color: $red;
    font-family: $karla;
  }

  &:hover {
    background: $red;

    .baseBtn__label {
      color: $white;
    }
  }

  &:hover {
    cursor: pointer;
  }

  &--green {
    border: 1px solid $greenDark;

    .baseBtn__label {
      color: $greenDark;
    }

    &:hover {
      background: $greenDark;
      .baseBtn__label {
        color: $white;
      }
    }
  }
}

/*------------------------------------------*/
// < 960px
@include breakpoint(l) {
  .baseBtn {
    padding: 14px 25px 14px 24px;

    &__label {
      font-size: 14px;
    }

    &--white {
      background: $blue;
      border: 1px solid $blue;

      .baseBtn__label {
        color: white;
      }

      &:hover {
        background: white;
        .baseBtn__label {
          color: $blue;
        }
      }
    }
  }
}
</style>
