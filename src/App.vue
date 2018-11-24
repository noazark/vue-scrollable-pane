<template>
  <div id="app">
    <div class="flex">
      <ScrollPane class="flex-el">
        <div class="table">
          <div class="field">
            <div class="cell" v-for="i in 1000" :key="i"></div>
          </div>
        </div>

        <transition name="glow" slot="top-indicator" slot-scope="s">
          <div class="indicator-top" v-if="!s.extreme"></div>
        </transition>

        <transition name="glow" slot="bottom-indicator" slot-scope="s">
          <div class="indicator-bottom" v-if="!s.extreme"></div>
        </transition>

        <transition name="glow" slot="left-indicator" slot-scope="s">
          <div class="indicator-left" v-if="!s.extreme"></div>
        </transition>

        <transition name="glow" slot="right-indicator" slot-scope="s">
          <div class="indicator-right" v-if="!s.extreme"></div>
        </transition>
      </ScrollPane>
    </div>
  </div>
</template>

<script>
import ScrollPane from './components/ScrollPane.vue'

export default {
  name: 'app',
  components: {
    ScrollPane
  }
}
</script>

<style>
:root {
  --background-color: #e6e5d9;
  --cell-color: #f9f8eb;
  --indicator: 40px;
}

body {
  margin: 0;
  background-color: var(--background-color);
}

.table {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 100%;
}

.field {
  --cells-x: 20;
  --cell-size: 50px;
  display: grid;
  grid-template-columns: repeat(var(--cells-x), var(--cell-size));
  grid-gap: 5px;
  grid-auto-rows: minmax(var(--cell-size), auto);
}

.field > .cell {
  background-color: var(--cell-color);
}

.flex {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.flex-el {
  height: 100%;
  width: 100%;
}

.indicator-top,
.indicator-bottom,
.indicator-left,
.indicator-right {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  pointer-events: none;
}

.indicator-top,
.indicator-bottom {
  left: -10px;
  right: -10px;
}

.indicator-left,
.indicator-right {
  top: -10px;
  bottom: -10px;
}

.indicator-top {
  bottom: initial;
  height: var(--indicator);
  margin-top: calc(-1 * var(--indicator));
  box-shadow:
    0 2px 3px 0px #b0f9f9,
    0 2px 6px #2bf3f3,
    0 4px 25px 10px #9ee6e65e;
}

.indicator-bottom {
  top: initial;
  height: var(--indicator);
  margin-bottom: calc(-1 * var(--indicator));
  box-shadow:
    0 -2px 3px 0px #b0f9f9,
    0 -2px 6px #2bf3f3,
    0 -4px 25px 10px #9ee6e65e;
}

.indicator-left {
  right: initial;
  width: var(--indicator);
  margin-left: calc(-1 * var(--indicator));
  box-shadow:
    2px 0 3px 0px #b0f9f9,
    2px 0 6px #2bf3f3,
    4px 0 25px 10px #9ee6e65e;
}

.indicator-right {
  left: initial;
  width: var(--indicator);
  margin-right: calc(-1 * var(--indicator));
  box-shadow:
    -2px 0 3px 0px #b0f9f9,
    -2px 0 6px #2bf3f3,
    -4px 0 25px 10px #9ee6e65e;
}

.glow-enter-active,
.glow-leave-active {
  transition-property: box-shadow;
  transition-duration: .6s;
  transition-timing-function: ease-out;
}

.glow-enter,
.glow-leave-to {
  box-shadow: 0 0 transparent;
}
</style>
