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
$backgroundLayers__Offset: 1.75rem * 7;
$backgroundLayers__Top: calc(#{$navigationHeight + $backgroundLayers__Offset});

$backgroundLayers__Left__Desktop: calc(50% - (#{$containerWidth} / 2) + 1.75rem);
$backgroundLayers__Left__Medium: 0.5rem * 5;
$backgroundLayers__Left__Mini: 0.25rem * 5;

$backgroundFill__Left: calc(50% - (#{$containerWidth} / 2) + (4 * 1.75rem));
$indentedFill__Left: calc(50% - (#{$containerWidth} / 2) + (14 * 1.75rem));
$indentedFill__Left__Medium: calc(50% - (#{$containerWidth} / 2) + (10 * 1.75rem));

// ///////////////////////////////////////////////////////////////////// General
.page-ecc-grants {
  color: $white;
}

.main-content {
  position: relative;
  padding-bottom: $backgroundLayers__Offset;
  @include mini {
    padding-bottom: calc(#{$backgroundLayers__Offset} - 7rem);
  }
}

#section_1 {
  padding-top: 0; // 1.75rem * 4
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
  @include medium {
    &:before {
      left: 2.5rem;
    }
    &:after {
      left: $indentedFill__Left__Medium;
    }
  }
  @include mini {
    &:before {
      border-radius: 0;
      left: 1.25rem;
    }
    &:after {
      left: 1.25rem;
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
  @include medium {
    &:before {
      left: $indentedFill__Left__Medium;
    }
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
    height: calc(100% + 5.5rem) !important;
  }
  @include medium {
    &:before {
      height: calc(100% + 4.625rem) !important;
    }
  }
  @include small {
    &:before {
      border-radius: 0 0 0 6.75rem;
    }
  }
  @include mini {
    &:before {
      height: calc(100% - 2.875rem) !important;
      border-radius: 0 0 0 4.75rem;
    }
  }
}

// /////////////////////////////////////////////////////////// Background Layers
::v-deep #page-ecc-grants-body-layer {
  position: absolute;
  top: -0.625rem;
  left: 0;
  width: 100%;
  height: calc(100% - 2rem);
  z-index: -11;
  .layer {
    border-radius: 0 0 0 11.5rem !important;
  }
  @include small {
    .layer {
      border-radius: 0 !important;
    }
  }
  @include mini {
    height: calc(100% + 2rem);
    left: -12rem;
    width: calc(100% + 24rem);
    // height: calc(100% + 32rem);
  }
}

#page-ecc-grants-background-layers {
  position: absolute;
  top: calc(-1 * #{$backgroundLayers__Offset});
  left: $backgroundLayers__Left__Desktop;
  width: calc(100% + 20rem);
  height: calc(100% + #{$backgroundLayers__Top / 2} - 2rem);
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
    padding: 0;
  }
  .image-block {
    width: 100vw;
    height: 20rem;
    transform: translateX(3rem);
    border-radius: 20rem 3rem 3rem 20rem;
    overflow: hidden;
    @include mini {
      transform: translateX(3rem);
    }
    @include tiny {
      transform: translateX(0rem);
    }
  }
  .image {
    width: 110%;
    transform: translateY(-1rem);
    @include small {
      width: 522px;
    }
    @include mini {
      // width: 22rem;
    }
  }
}

::v-deep #logos {
  padding: 5.375rem 0;
  @include mini {
    padding: 1.5rem 0;
  }
}

::v-deep #hero {
  padding: 0;
  margin-bottom: 1.5rem;
  @include mini {
    margin-bottom: 0;
    margin-top: 1rem;
    padding-bottom: 3rem;
  }
  .column-content {
    &.left {
      display: flex;
      margin-right: 1.25rem;
      .label {
        margin-bottom: 1rem;
        letter-spacing: 0.025rem;
        line-height: leading(35, 13);
        @include fontWeight_SemiBold;
      }
      .heading {
        margin-bottom: 1rem;
        @include fontSize_Huge;
        @include fontWeight_Medium;
        letter-spacing: 0.0625rem;
        line-height: leading(66, 55);
        @include medium {
          @include fontSize_ExtraExtraLarge;
        }
        @include mini {
          @include fontSize_ExtraExtraLarge;
          margin: 0;
        }
      }
      .subheading {
        margin-bottom: 2rem;
        @include fontSize_Large;
        @include fontWeight_Regular;
        letter-spacing: 0.0375rem;
        line-height: leading(30, 20);
        @include mini {
          @include fontSize_Medium;
        }
      }
      .button {
        padding: 0.5rem 1.125rem 0.625rem;
        font-size: 0.9375rem;
        @include fontWeight_Medium;
        letter-spacing: kerning(0.45);
        line-height: leading(22.5, 15);
        transition: all 350ms ease;

        @include medium {
          margin-bottom: 1.5rem;
        }

        .text {
          margin-right: 0.5rem;
          transition: inherit;
          white-space: nowrap;
        }
        .chevron {
          margin: 0 0 -0.0625rem 0.25rem;
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
          transform: scale(1.05);
          .chevron {
            margin-left: 0.625rem;
          }
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
        width: 40rem;
        // max-width: 38rem;
        min-height: 20rem;
        border-radius: 20vw 3rem 3rem 20vw;
        overflow: hidden;
        @include medium {
          width: 100vw;
          border-radius: 20rem 3rem 3rem 20rem;
        }
      }
      .image {
        width: 110%;
        width: 46rem;
        transform: translate(-3rem, -4rem);
        @include xlarge {
          width: 42rem;
        }
        @include medium {
          width: 36rem;
          transform: 0;
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
    @include mini {
      @include fontSize_Medium;
    }
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
    max-width: 56rem;
    max-height: 21.875rem;
    border-radius: 25vw 3rem 3rem 25vw;
    overflow: hidden;
    transform: translateX(3.5rem);
    @include medium {
      width: 100vw;
      max-height: 50vw;
      transform: translateX(-4rem);
    }
    @include mini {
      transform: translateX(0);
    }
  }
  .image {
    width: 100%;
    max-width: 56rem;
    transform: translateY(-13%);
    @include mini {
      transform: translateY(-10%);
    }
  }
}

::v-deep #section-2-heading {
  padding-top: 7.875rem;
  padding-bottom: 0;
  margin-bottom: 0;

  @include mini {
    padding-top: 3rem;
  }

  .image-block {
    transform: translate(-1.5rem, -2.25rem);
    @include small {
      transform: translate(-1.5rem, 0);
    }
    @include mini {
      margin-top: 2rem;
      transform: translate(0, 0);
    }
  }
  .image {
    width: 12.125rem;
    @include small {
      width: 9rem;
      margin: 0 auto;
    }
    @include mini {
      margin-right: 0;
      margin-bottom: 0.5rem;
      width: 8rem;
    }
  }
  .heading {
    margin-bottom: 0;
    @include fontSize_Huge;
    @include fontWeight_Medium;
    letter-spacing: 0.0625rem;
    line-height: leading(66, 55);
    @include medium {
      margin-bottom: 3rem;
    }
    @include mini {
      margin-bottom: 0;
      @include fontSize_ExtraExtraLarge;
      text-align: right;
    }
  }
  .button-row {
    margin: 0;
  }
  .right {
    .image-block {
      display: none;
      @include mini {
        display: block;
      }
    }
  }
}

::v-deep #section-2-accordion {
  padding: 0;
  padding-bottom: 5rem;
  @include mini {
    padding-top: 1.5rem;
    margin-bottom: 0;
    padding-bottom: 3rem;
  }
}

// ----------------------------------------------------------------- [Section] 3
::v-deep #section-3-banner-image {
  padding: 0;
  .image-block {
    width: 74vw;
    max-width: 56rem;
    max-height: 21.875rem;
    border-radius: 22vw 3rem 3rem 22vw;
    overflow: hidden;
    @include medium {
      width: 100vw;
      transform: translateX(-4rem);
    }
    @include mini {
      width: 100vw;
      max-height: 50vw;
      transform: translateX(0);
    }
  }
  .image {
    width: 100%;
    max-width: 56rem;
    transform: translateY(-13%);
  }
}

::v-deep #section-3-text-block {
  padding-top: 6.5625rem;
  padding-bottom: 3.625rem;

  @include mini {
    padding-top: 4.5rem;
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
}

::v-deep #section-3-accordion {
  padding-top: 0;
  @include mini {
    padding-bottom: 3rem;
  }
}

// ----------------------------------------------------------------- [Section] 4
::v-deep #section-footer {
  padding-top: 1rem;
  padding-bottom: 2.75rem;
  @include mini {
    padding-bottom: 7rem;
  }
  .image-block {
    padding: 0 2.5rem;
    @include medium {
      padding-left: 0;
    }
    @include mini {
      padding: 0;
      // padding-left: 1rem;
      margin-bottom: 1.5rem;
    }
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
      @include mini {
        @include fontSize_Large;
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
      @include mini {
        @include fontSize_Medium;
      }
    }
  }
}

</style>
