<script>
export default {
  name: 'ButtonCore',

  props: {
    to: {
      type: [String, Object, Boolean],
      default: false,
    },
    href: {
      type: [String, Boolean],
      default: false,
    },
  },

  computed: {
    tag () {
      if (this.to) {
        return 'router-link'
      }
      else if (this.href) {
        return 'a'
      }
      else {
        return 'button'
      }
    },
  },

}
</script>

<template>
<component
  :is="tag"
  class="button-core"
  :href="href"
  :to="to"
>
  <slot></slot>
</component>
</template>

<style lang="sass" scoped>
@import '../../sass/variables'
@import '../../sass/core/mixins'

//
// Color Mixin
// --------------------------------------------------

@mixin color($primary: $button-background, $secondary: $button-text-color)
  background: $primary
  color: $secondary

  &:hover
    background: mix($primary, $secondary, 90%)
    color: $secondary

  &:active,
  &.active
    background: mix($primary, $secondary, 88%)
    color: $secondary

  &.light
    background: transparent
    box-shadow: none
    color: $primary
    padding-left: 0
    padding-right: 0

    &:hover
      color: mix($primary, $secondary, 80%)

    &:active,
    &.active
      color: mix($primary, $secondary, 70%)

//
// Button Core
// --------------------------------------------------

.button-core
  position: relative
  transition: background-color $time--small
  box-shadow: $shadow--large
  line-height: 1.1
  text-align: center
  +color()
  // +color($color-gray)

//
// Variants
// --------------------------------------------------

.primary
  +color($color-primary)

.secondary
  +color($color-secondary)

.success
  +color($color-success)

.warning
  +color($color-warning)

.danger
  +color($color-danger)

.info
  +color($color-info)

.small
  font-size: .8em

.large
  font-size: 1.3em
  min-width: 15rem

.circle
  +center()
  border-radius: 50%
  height: 2.75em
  padding: 0
  width: 2.75em

.icon
  +chain(2.5em)
  display: inline-flex

.multiline /deep/

  div + div
    font-size: .7em
    font-weight: 300
    text-transform: none

</style>
