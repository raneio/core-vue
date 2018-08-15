<script>
export default {
  name: 'ImageCore',

  props: {
    src: {
      type: [Object, String],
      required: true,
    },
    alt: {
      type: String,
      required: true,
    },
  },

  data () {
    return {
      loaded: false,
      placeholderStyle: null,
    }
  },

  computed: {

    isPlaceholder () {
      return this.src.width > 0 && this.src.height > 0
    },

    placeholderSrc () {
      return this.src.placeholder || 'data:image/gif;base64,R0lGODlhAQABAAD/ACwAAAAAAQABAAACADs='
    },

    imgScr () {
      return this.src.url || this.src
    },

  },

  methods: {

    loadImage () {
      let image = new Image()

      image.onload = () => {
        this.loaded = true
      }

      image.onerror = () => {
        console.warn('Image loading faild:', this.imgScr)
      }

      image.src = this.imgScr
    },

    setPlaceholderStyle () {
      if (!this.isPlaceholder) return null

      let blur = Math.max(this.$refs.placeholder.width, this.$refs.placeholder.height) / 50
      if (blur < 3) blur = 3
      if (blur > 20) blur = 20
      this.placeholderStyle = {
        filter: `blur(${blur}px)`,
      }
    },

  },

  mounted () {
    this.loadImage()
    this.setPlaceholderStyle()
  },

}
</script>

<template>
<figure
  class="image-core"
  :class="{
    'loading': loaded === false,
    'loaded': loaded === true,
  }"
>

  <img
    ref="placeholder"
    class="placeholder"
    :src="placeholderSrc"
    :width="src.width"
    :height="src.height"
    :style="placeholderStyle"
    v-if="isPlaceholder"
  >

  <img
    class="image"
    :src="imgScr"
    :alt="alt"
  >
</figure>
</template>

<style lang="sass" scoped>
@import '../../sass/variables'
@import '../../sass/core/mixins'

//
// Image Core
// --------------------------------------------------

.image-core
  display: inline-block
  max-height: 100%
  max-width: 100%
  overflow: hidden
  position: relative

  .placeholder
    position: relative
    transform: scale(1.1)
    transition: opacity $time $time/4

    + .image
      position: absolute
      transform: translateX(-100%)

  .image
    max-width: 100%
    transition: opacity $time
    opacity: 0

.image-core.loaded

  .placeholder
    opacity: 0

  .image
    opacity: 1

//
// Variants
// --------------------------------------------------

.shadow
  box-shadow: $shadow--large

</style>
