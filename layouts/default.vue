<template>
  <div class="master-container">

    <nuxt />

  </div>
</template>

<script>
// ===================================================================== Imports
import SiteNavigation from '@/components/SiteNavigation'
import SiteFooter from '@/components/SiteFooter'

// ====================================================================== Export
export default {
  name: 'LayoutDefault',

  components: {
    SiteNavigation,
    SiteFooter
  },

  mounted () {
    const hash = this.$route.hash.replace('#', '')
    if (hash) {
      const element = document.getElementById(hash) || document.querySelector(`[data-id='${hash}']`)
      if (element) {
        this.$scrollToElement(element, 0, -50)
      }
    }
  }
}
</script>
