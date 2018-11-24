<template>
  <div class="wrapper">
    <div class="container" ref="container" @scroll="setScrollStyle">
      <slot/>
    </div>

    <slot name="top-indicator" :extreme="extremes.top"/>
    <slot name="right-indicator" :extreme="extremes.right"/>
    <slot name="bottom-indicator" :extreme="extremes.bottom"/>
    <slot name="left-indicator" :extreme="extremes.left"/>
  </div>
</template>

<script>
export default {
  name: 'ScrollPane',

  data () {
    return {
      extremes: {
        top: true,
        bottom: true,
        right: true,
        left: true
      }
    }
  },

  mounted() {
    this.setScrollStyle()
  },

  methods: {
    setScrollStyle() {
      const {
        clientWidth,
        clientHeight,
        scrollHeight,
        scrollLeft,
        scrollTop,
        scrollWidth,
      } = this.$refs.container

      this.extremes.top = scrollTop === 0
      this.extremes.right = scrollLeft + clientWidth === scrollWidth
      this.extremes.bottom = scrollTop + clientHeight === scrollHeight
      this.extremes.left = scrollLeft === 0
    }
  }
}
</script>

<style scoped>
.wrapper {
  position: relative;
  overflow: hidden;
}

.container {
  overflow: scroll;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
}
</style>