<template>
  <div class="page page-ecc-grants">

    <div class="main-content">

      <PageSection
        v-for="(section, key) in sections"
        :id="key"
        :key="key"
        :section="section" />

      <BackgroundLayers
        id="page-ecc-grants-body-layer"
        layers-array="2"
        :breakpoints="{ mini: { stroke: 0.25, radius: 5 } }" />

      <BackgroundLayers
        id="page-ecc-grants-background-layers"
        layers-array="6_5_4_3"
        :reverse="true"
        :breakpoints="pageLayersBreakpointData" />

    </div>

  </div>
</template>

<script>
// ====================================================================== Import
import { mapGetters } from 'vuex'
import CloneDeep from 'lodash/cloneDeep'

import ECCGrantsPageData from '@/content/pages/ecc-grants.json'

import PageSection from '@/components/PageSection'
import BackgroundLayers from '@/components/BackgroundLayers'

// ====================================================================== Export
export default {
  name: 'PageECCGrants',

  components: {
    PageSection,
    BackgroundLayers
  },

  data () {
    return {
      tag: 'ecc_grants',
      scroll: false,
      resize: false,
      pageLayersBreakpointData: {
        medium: {
          stroke: 0.5,
          radius: 12.75
        },
        mini: {
          stroke: 0.25,
          radius: 5
        }
      }
    }
  },

  async fetch ({ store }) {
    await store.dispatch('global/getBaseData', 'general')
    await store.dispatch('global/getBaseData', { key: 'ecc_grants', data: ECCGrantsPageData })
  },

  head () {
    return this.$CompileSeo(this.$GetSeo(this.tag))
  },

  computed: {
    ...mapGetters({
      siteContent: 'global/siteContent'
    }),
    sections () {
      const content = CloneDeep(this.siteContent.ecc_grants.page_content)
      return content
    }
  }
}
</script>

<style lang="scss" scoped>
$backgroundLayers__Offset: 1.75rem * 5;
$backgroundLayers__Top: calc(#{$navigationHeight + $backgroundLayers__Offset});

$backgroundLayers__Left__Desktop: calc(50% - (#{$containerWidth} / 2) + 1.75rem);
$backgroundLayers__Left__Medium: 0.5rem * 5;
$backgroundLayers__Left__Mini: 0.25rem * 5;

$backgroundFill__Left: calc(50% - (#{$containerWidth} / 2) + (4 * 1.75rem));
$indentedFill__Left: calc(50% - (#{$containerWidth} / 2) + (14 * 1.75rem));

// ///////////////////////////////////////////////////////////////////// General
.page-ecc-grants {
  // padding-bottom: calc(#{$backgroundLayers__Top} + 10rem);
  color: $white;
}

.main-content {
  position: relative;
  top: -2.5 * $backgroundLayers__Offset;
}

#section_0 {
  margin-bottom: $backgroundLayers__Offset - $navigationHeight;
}

#section_1 {
  padding-top: 7rem; // 1.75rem * 4
  &:before {
    content: '';
    position: absolute;
    top: 0;
    left: $backgroundFill__Left;
    width: calc(100% + 3.5rem);
    height: calc(100% - 18rem);
    background-color: $blackPearl;
    border-radius: 0 0 0 8.5rem;
    filter: drop-shadow(0 0 0.4rem rgba(0, 0, 0, 0.1));
    z-index: -1;
  }
  &:after {
    content: '';
    position: absolute;
    bottom: 0;
    left: $indentedFill__Left;
    width: calc(100% + 3.5rem);
    height: 100%;
    background-color: $blackPearl;
    filter: drop-shadow(0 0 0.4rem rgba(0, 0, 0, 0.1));
    z-index: -1;
  }
  @include small {
    &:before {
      left: 1.25rem;
    }
  }
  @include mini {
    &:before {
      border-radius: 0;
    }
  }
}

#section_2,
#section_3,
#section_4 {
  &:before {
    content: '';
    position: absolute;
    top: 0;
    left: $indentedFill__Left;
    width: calc(100% + 3.5rem);
    height: calc(100% + 1.5rem);
    background-color: $blackPearl;
    filter: drop-shadow(0 0 0.4rem rgba(0, 0, 0, 0.1));
    z-index: -10;
  }
  @include mini {
    &:before {
      left: 1.25rem;
    }
  }
}
#section_3,
#section_4 {
  z-index: 1;
}

#section_2 {
  padding-top: 1.25rem;
  &:before {
    height: 100%;
  }
}

#section_4 {
  &:before {
    height: calc(100% + 5.375rem) !important;
  }
}

// /////////////////////////////////////////////////////////// Background Layers
::v-deep #page-ecc-grants-body-layer {
  position: absolute;
  top: 0;
  left: 0;
  width: calc(100% + 16rem);
  height: calc(100% + #{$backgroundLayers__Top / 2} + 1.75rem * 2);
  z-index: -11;
  @include small {
    .layer {
      border-radius: 0 !important;
    }
  }
  @include mini {
    left: -12rem;
    width: calc(100% + 24rem);
  }
}

#page-ecc-grants-background-layers {
  position: absolute;
  top: 0;
  left: $backgroundLayers__Left__Desktop;
  width: calc(100% + 20rem);
  height: calc(100% + #{$backgroundLayers__Top / 2} - 1.75rem * 2);
  @include medium {
    left: $backgroundLayers__Left__Medium;
  }
  @include mini {
    left: $backgroundLayers__Left__Mini;
  }
}

// ////////////////////////////////////////////////////// Section Customizations
// ----------------------------------------------------------------- [Section] 1
::v-deep #mobile_image_banner {
  display: none;
  @include mini {
    display: block;
    padding: 0 0 2.625rem 0;
    .image {
      width: 100vw;
      border-radius: 50vw 0 0 50vw;
    }
  }
}

::v-deep #logos {
  padding-top: 10rem;
  padding-bottom: 1.5rem;
}

::v-deep #hero {
  padding: 0;
  margin-bottom: 0.5rem;
  @include mini {
    margin-bottom: 0;
  }
  .column-content {
    &.left {
      display: flex;
      margin-right: 0.125rem 1.25rem;
      .heading {
        margin-bottom: 2rem;
        @include fontSize_Huge;
        @include fontWeight_Medium;
        letter-spacing: 0.0625rem;
        line-height: leading(66, 55);
        @include small {
          @include fontSize_ExtraExtraLarge;
        }
        @include tiny {
          margin: 0;
        }
      }
      .button {
        padding: 0 1.125rem;
        font-size: 0.9375rem;
        @include fontWeight_Medium;
        letter-spacing: kerning(0.45);
        line-height: leading(35, 15);
        transition: 250ms ease;
        .text {
          margin-right: 0.5rem;
          transition: inherit;
        }
        .chevron {
          margin-right: 0;
          transform: rotate(-90deg);
          transition: inherit;
          svg {
            transition: inherit;
            width: 0.625rem;
          }
          path {
            transition: inherit;
          }
        }
        &:hover {
          border-color: $azureRadiance;
        }
        &:active {
          border-color: $azureRadiance;
          color: $azureRadiance;
          svg,
          path {
            stroke: $azureRadiance;
          }
        }
      }
    }
    &.right {
      margin-left: 0.75rem;
      .image-block {
        transform: translateY(-3.5rem);
        max-height: 20rem;
        width: 38vw;
        max-width: 53.5rem;
        min-height: 20rem;
        border-radius: 20vw 3rem 3rem 20vw;
        overflow: hidden;
      }
      .image {
        width: 105%;
        max-width: 53.5rem;
        transform: translateY(-3rem);
        @include xlarge {
          transform: translateY(0);
          width: 110%;
        }
        @include large {
          width: 50vw;
        }
        @include medium {
          width: 50vw;
          // border-radius: 25vw 0 0 25vw;
        }
      }
    }
  }
}

::v-deep #hero_text {
  padding-top: 0;
  padding-bottom: 4.25rem;
  text-align: left;

  .subheading {
    margin-bottom: 1.5rem;
    @include fontSize_Large;
    @include fontWeight_Regular;
    letter-spacing: 0.0375rem;
    line-height: leading(30, 20);
  }

  .description {
    @include fontSize_Regular;
    @include fontWeight_Regular;
    letter-spacing: kerning(0.48);
    line-height: leading(24, 16);
    a {
      @include linkInText;
    }
  }

  @include mini {
    text-align: left;
    margin-bottom: 0;
  }
}
// ----------------------------------------------------------------- [Section] 2
::v-deep #section-2-banner-image {
  padding: 0;
  .image-block {
    width: 64vw;
    max-width: 80.875rem;
    max-height: 21.875rem;
    border-radius: 22vw 3rem 3rem 22vw;
    overflow: hidden;
    transform: translateX(3.5rem);
  }
  .image {
    width: 100%;
    max-width: 80.875rem;
    transform: translateY(-13%);
    @include mini {
      width: 90vw;
      border-radius: 50vw 0 0 50vw;
    }
  }
}

::v-deep #section-2-heading {
  padding-top: 7.875rem;
  padding-bottom: 0;
  margin-bottom: 0;
  .image-block {
    transform: translate(-1.5rem, -2.25rem);
  }
  .image {
    width: 12.125rem;
  }
  .heading {
    margin-bottom: 0;
    @include fontSize_Huge;
    @include fontWeight_Medium;
    letter-spacing: 0.0625rem;
    line-height: leading(66, 55);
  }
  .button-row {
    margin: 0;
  }
}

::v-deep #section-2-accordion {
  padding: 0;
  padding-bottom: 5rem;
  @include mini {
    padding-top: 1.5rem;
    margin-bottom: 0;
  }
}

// ----------------------------------------------------------------- [Section] 3
::v-deep #section-3-banner-image {
  padding: 0;
  .image-block {
    width: 74vw;
    max-width: 80.875rem;
    max-height: 21.875rem;
    border-radius: 22vw 3rem 3rem 22vw;
    overflow: hidden;
  }
  .image {
    width: 100%;
    max-width: 80.875rem;
    transform: translateY(-13%);
    @include mini {
      width: 140vw;
      border-radius: 70vw 0 0 70vw;
    }
  }
}

::v-deep #section-3-text-block {
  padding-top: 6.5625rem;
  padding-bottom: 3.625rem;
  .description {
    @include fontSize_Regular;
    @include fontWeight_Regular;
    letter-spacing: kerning(0.48);
    line-height: leading(24, 16);
    a {
      @include linkInText;
    }
  }
}

::v-deep #section-3-accordion {
  padding-top: 0;
}

// ----------------------------------------------------------------- [Section] 4
::v-deep #section-footer {
  padding-top: 1rem;
  padding-bottom: 2.75rem;
  .image-block {
    padding: 0 2.5rem;
  }
  .text-block {
    .heading {
      margin-bottom: 1.625rem;
      @include fontSize_ExtraLarge;
      @include fontWeight_Medium;
      letter-spacing: kerning(0.48);
      line-height: leading(35, 24);
      a {
        @include linkInText;
      }
    }
    .description {
      @include fontSize_Large;
      @include fontWeight_Regular;
      letter-spacing: kerning(0.6);
      line-height: leading(30, 20);
      a {
        @include linkInText;
      }
    }
  }
}

</style>
