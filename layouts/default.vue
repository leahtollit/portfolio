<template>
  <div class="theSite">
    <GlobalHeader />
    <nuxt />
    <GlobalFooter />
    <MobileMenu />
    <MobileBtn />
    <ModalBase v-if="modal.type" />
    <GlobalAlert v-if="global.alert.type" :type="global.alert.type" :text="global.alert.message" />
    <GlobalTransition />
    <GlobalPreloader />
  </div>
</template>

<script>
import { mapState } from 'vuex'
// import { firebase } from '~/mixins/firebase'
// import { web3 } from '~/mixins/web3'

export default {
  name: 'LayoutDefault',
  mixins: [
    // firebase
    // web3
  ],
  computed: {
    ...mapState(['global', 'modal'])
  },
  mounted() {
    // setupFirebase
    this.$store.dispatch('global/updateCurrentPage', this.$route.path)
  }
}
</script>
