<script>
export default {
  name: 'HeadingCore',
}
</script>

<template>
<header class="heading-core">
  <slot></slot>
</header>
</template>

<style lang="sass" scoped>
@import '../../sass/variables'
@import '../../sass/core/mixins'

//
// Heading Core
// --------------------------------------------------

.heading-core
  +gap(.5rem)

  +hx
    font-size: 2.5rem
    line-height: 1

//
// Variants
// --------------------------------------------------

.primary
  position: relative
  +gap(0)

  +hx
    font-weight: 700
    line-height: .95
    color: $color-primary

  .content
    position: relative
    +mask('/img/editlayer-text-mask.jpg', $color-primary)
    // text-shadow: -.05em -.05em white

  .shadow
    position: absolute
    top: 0
    left: 0
    right: 0
    bottom: 0
    text-shadow: -.04em -.04em $color-white, $shadow-heading

  .tagline
    position: relative

// .secondary
//   +hx
//     font-size: 2.5rem

.small
  +hx
    font-size: 1.5rem

.large
  +hx
    font-size: 4.75rem

.light
  font-weight: 300
  text-transform: none

</style>
