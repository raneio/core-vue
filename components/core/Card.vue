<script>
export default {
  name: 'CardCore',

  computed: {

    isHeader () {
      return !!this.$slots.header
    },

    isMain () {
      return !!this.$slots.main
    },

    isFooter () {
      return !!this.$slots.footer
    },

  },

}
</script>

<template>
<section class="card-core">
  <header class="header" v-if="isHeader">
    <slot name="header"></slot>
  </header>

  <main class="main" v-if="isMain">
    <slot name="main"></slot>
  </main>

  <footer class="footer" v-if="isFooter">
    <slot name="footer"></slot>
  </footer>
</section>
</template>

<style lang="sass" scoped>
@import '../../sass/variables'
@import '../../sass/core/mixins'

//
// Card Core
// --------------------------------------------------

.card-core
  box-shadow: $shadow--large, $shadow-inner
  background-color: $background-color
  width: 100%
  border-radius: $radius
  transition: box-shadow $time--small

  .header,
  .footer,
    +chain(1em)
    padding: 1em 1.5rem

  .header
    border-top-left-radius: $radius
    border-top-right-radius: $radius
    background-color: $color-gray--lightest
    border-bottom: 1px solid $color-gray--lighter

    +hx
      font-size: 1.25em
      font-weight: 400
      overflow: hidden
      text-overflow: ellipsis
      white-space: nowrap

    &:last-child
      border-bottom: 0

  .main
    padding: 1.5rem

  .footer
    border-bottom-left-radius: $radius
    border-bottom-right-radius: $radius

//
// Variants
// --------------------------------------------------

.link:hover
  cursor: pointer

.small
  font-size: .8rem

  .header
    +hx
      font-weight: 600
</style>
