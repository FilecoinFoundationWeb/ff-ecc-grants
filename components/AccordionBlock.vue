<template>
  <div :class="['block accordion-block', `theme__${theme}`]">

    <Zero_Core__Accordion
      v-slot="{ active }"
      :multiple="multiple">
      <Zero_Core__Accordion_Section
        v-for="(section, index) in sections"
        :key="index"
        :active="active">

        <Zero_Core__Accordion_Header>
          <div class="label">
            {{ section.label }}
          </div>
          <IconArrowDown class="icon" />
        </Zero_Core__Accordion_Header>

        <Zero_Core__Accordion_Content>
          <div
            :class="['accordion-content-wrapper', 'basic-accordion-content', theme]"
            v-html="section.content">
          </div>
        </Zero_Core__Accordion_Content>

      </Zero_Core__Accordion_Section>
    </Zero_Core__Accordion>

  </div>
</template>

<script>
// ===================================================================== Imports
import IconArrowDown from '@/components/icons/Chevron'

// ====================================================================== Export
export default {
  name: 'AccordionBlock',

  components: {
    IconArrowDown
  },

  props: {
    block: {
      type: Object,
      required: true
    }
  },

  computed: {
    sections () {
      return this.block.sections
    },
    multiple () {
      return this.block.multiple
    },
    theme () {
      return this.block.theme || ''
    }
  }
}
</script>

<style lang="scss" scoped>
// ///////////////////////////////////////////////////////////////////// General
.accordion-block {
  position: relative;
}

// ///////////////////////////////////////////////////////////////////// Section
.accordion-section {
  margin-bottom: 1.5rem;
  &.open {
    .icon {
      transform: rotate(180deg);
    }
  }
}

// ////////////////////////////////////////////////////////////////////// Header
.accordion-header {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
  margin-bottom: 1rem;
  @include fontSize_ExtraLarge;
  @include fontWeight_Medium;
  letter-spacing: kerning(0.48);
  line-height: leading(35, 24);
}

::v-deep .basic-accordion-content {
  @include fontSize_Regular;
  @include fontWeight_Regular;
  letter-spacing: kerning(0.48);
  line-height: leading(24, 16);
  a {
    @include linkInText;
  }
  .accordion-content-heading {
    display: inline-block;
    margin-top: 0.75rem;
    font-size: 1.25rem;
    @include fontWeight_Medium;
    letter-spacing: kerning(0.48);
    line-height: leading(35, 20);
  }
}

.label {
  padding-right: 3rem;
}

.icon {
  width: 1rem;
  transition: 250ms ease-in-out;
}

// ///////////////////////////////////////////////////////////////////// Content
::v-deep .accordion-content-wrapper {
  padding-bottom: 2rem;
}
</style>
