<template>
  <component
    :is="tag"
    :to="getTo()"
    :href="getHref()"
    :target="getTarget()"
    :class="['button', getType()]"
    :disabled="disabled"
    @click="clickHandler">

    <Zero_Core__Loader_TripleDot :class="{ show: loading }" />

    <div :class="['button-content', { hide: loading }]">

      <div v-if="iconBefore" class="icon">
        <slot name="icon-before"></slot>
      </div>

      <p v-if="text" :class="{ 'item-after': iconBefore }">
        {{ text }}
      </p>

      <div v-if="iconAfter" class="item-after">
        <slot name="icon-after"></slot>
      </div>

    </div>

  </component>
</template>

<script>
// ===================================================================== Imports
import { mapGetters, mapActions } from 'vuex'

// ===================================================================== Functions
const checkSlots = (instance) => {
  const slots = instance.$slots
  if (slots.hasOwnProperty('icon-before') && slots['icon-before']) { instance.iconBefore = true }
  if (slots.hasOwnProperty('icon-after') && slots['icon-after']) { instance.iconAfter = true }
}

// ====================================================================== Export
export default {
  name: 'Button',

  props: {
    type: { // A, B, C, D
      type: String,
      required: false,
      default: 'A'
    },
    tag: { // button or nuxt-link
      type: String,
      required: false,
      default: 'button'
    },
    to: {
      type: [String, Boolean],
      required: false,
      default: false
    },
    target: {
      type: [String, Boolean],
      required: false,
      default: false
    },
    loader: {
      type: [String, Boolean],
      required: false,
      default: false
    },
    text: {
      type: String,
      required: false,
      default: ''
    },
    disabled: {
      type: Boolean,
      required: false,
      default: false
    }
  },

  data () {
    return {
      iconBefore: false,
      iconAfter: false
    }
  },

  computed: {
    ...mapGetters({
      loaders: 'core/loaders'
    }),
    loading () {
      return this.loaders.find(obj => obj === this.loader)
    }
  },

  mounted () {
    checkSlots(this)
  },

  methods: {
    ...mapActions({
      addLoader: 'core/addLoader'
    }),
    clickHandler () {
      const loader = this.loader
      if (typeof loader === 'string') {
        this.addLoader(loader)
      }
      this.$emit('clicked')
    },
    getTo () {
      return this.tag === 'nuxt-link' ? this.to : false
    },
    getHref () {
      return this.tag === 'a' ? this.to : false
    },
    getTarget () {
      const tag = this.tag
      return (tag === 'nuxt-link' || tag === 'a') ? this.target : false
    },
    getType () {
      return `type-${this.type}`
    }
  }
}
</script>

<style lang="scss" scoped>
// ///////////////////////////////////////////////////////////////////// General
.button {
  position: relative;
  height: 2.25rem;
  cursor: pointer;
}

.triple-dot-loader,
.button-content {
  width: 100%;
  height: 100%;
}

.triple-dot-loader {
  position: absolute;
  top: 0;
  left: 0;
  opacity: 0;
  &.show {
    opacity: 1;
  }
}

.button-content {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 0.5rem;
  &.hide {
    opacity: 0;
  }
}

.item-after {
  margin-left: 0.75rem;
}

.icon {
  display: inline-block;
  height: 0.7rem;
  margin: auto;
}

// /////////////////////////////////////////////////////////////// [Type] Common
.type-A,
.type-B,
.type-C,
.type-D {
  white-space: nowrap;
  padding: 0 0.75rem;
  &:not(:disabled) {

  }
  &:disabled {
    background-color: $gray300;
    cursor: no-drop;
  }
}

// //////////////////////////////////////////////////////////////////// [Type] A
.type-A {

}

// //////////////////////////////////////////////////////////////////// [Type] B
.type-B {

}

// //////////////////////////////////////////////////////////////////// [Type] A
.type-C {

}

// //////////////////////////////////////////////////////////////////// [Type] A
.type-D {

}
</style>
