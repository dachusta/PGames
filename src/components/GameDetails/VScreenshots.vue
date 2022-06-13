<template>
  <div class="screenshots">
    <img class="screenshots__display" :src="screenshot" alt="1" />
    <div
      class="screenshots__list"
      ref="screenshotsList"
      @mousedown="startScroll"
      @mousemove="moveScroll"
      @mouseup="endScroll"
      @mouseleave="endScroll"
    >
      <img
        v-for="screenshotItem in props.list"
        :key="screenshotItem.id"
        class="screenshots__item"
        :class="{ selected: screenshot === screenshotItem.image }"
        :src="screenshotItem.image"
        :alt="screenshotItem.id"
        @click="setScreenshot(screenshotItem.image)"
        @mousedown.prevent
      />
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
// eslint-disable-next-line
const props = defineProps({
  list: {
    type: Array,
    required: true
  }
})

const selectedScreenshot = ref(null)

function setScreenshot (src) {
  selectedScreenshot.value = src
}

const screenshot = computed(() => {
  return selectedScreenshot.value
    ? selectedScreenshot.value
    : props?.list?.[0]?.image
})

//
// // // //
// Drag Scroll ================================
// // // //
//

const screenshotsList = ref(null)

// eslint-disable-next-line prefer-const
let isDrag = ref(false)

function startScroll () {
  isDrag.value = true
}
function moveScroll (params) {
  if (!isDrag.value) return

  screenshotsList.value.scrollTo(
    screenshotsList.value.scrollLeft - params.movementX,
    0
  )
}
function endScroll () {
  isDrag.value = false
}
</script>

<style lang="scss" scoped>
.screenshots {
  background: rgba(60, 68, 100, 0.7);

  &__display {
    width: 640px;
    height: 360px;
    object-fit: contain;
    background: black;
  }

  &__list {
    display: flex;
    gap: 3px;
    overflow: auto;
    padding: 3px;
  }

  &__item {
    width: 128px;
    height: 72px;
    border: 2px solid rgba(60, 68, 100, 0.7);
    cursor: pointer;
    object-fit: contain;
    background: black;
    transition: border 0.2s ease;

    &.selected {
      border: 2px solid #cbdbee;
    }
  }
}
</style>
