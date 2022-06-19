<template>
  <div class="screenshots">
    <img
      class="screenshots__display"
      :src="screenshot"
      alt="1"
      @click="showFullScreen()"
    >
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

    <div
      v-if="isFullScreen"
      class="full-screen__wrap"
      @click="hideFullScreen()"
    >
      <div v-if="isFullScreen" class="full-screen"  @click.stop>
        <header class="full-screen__header">
          <button
            class="btn-close"
            @click="hideFullScreen()"
          >
            <IconClose />
          </button>
        </header>
        <main class="main">
          <img :src="screenshot" alt="0">
        </main>
        <footer class="full-screen__footer">
          <button class="btn-prev" @click="prevScreen">Prev</button>
          {{ screenIndex + 1 }} of {{ list.length }} screenshots
          <button class="btn-next" @click="nextScreen">Next</button>
        </footer>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import IconClose from '@/components/icons/IconClose.vue'

// eslint-disable-next-line
const emit = defineEmits(['isFullScreen'])

// eslint-disable-next-line
const props = defineProps({
  list: {
    type: Array,
    required: true,
    default: () => []
  }
})

const selectedScreenshot = ref(null)

function setScreenshot (src) {
  selectedScreenshot.value = src
}

const screenshot = computed(() => {
  return selectedScreenshot.value
    ? selectedScreenshot.value
    : props.list[0]?.image
})

//
// // // //
// Drag Scroll ================================
// // // //
//

// переименовать? screenshotListElem
const screenshotsList = ref(null)

const isDrag = ref(false)

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

// ***********************
const isFullScreen = ref(true)
const screenIndex = ref(0)

const showFullScreen = () => {
  isFullScreen.value = true
  screenIndex.value = props.list.findIndex(e => e.image === screenshot.value)
  emit('isFullScreen', isFullScreen.value)
}
const nextScreen = () => {
  if (!props.list.length || screenIndex.value >= props.list.length - 1) return

  screenIndex.value++
  setScreenshot(props.list[screenIndex.value].image)
}
const prevScreen = () => {
  if (!props.list.length || screenIndex.value <= 0) return

  screenIndex.value--
  setScreenshot(props.list[screenIndex.value].image)
}
const hideFullScreen = () => {
  isFullScreen.value = false
  emit('isFullScreen', isFullScreen.value)
}
// const findIndex = ref(props.list.findIndex(e => e.image === screenshot.value))
// console.log(findIndex)
</script>

<style lang="scss" scoped>
.screenshots {
  position: relative;
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

  .full-screen__wrap {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background: rgba(0, 0, 0, 0.7);
    z-index: 1000;
  }
  .full-screen {
    position: fixed;
    top: 50%;
    left: 50%;
    display: grid;
    padding: 10px 20px;
    background: #27293f;
    transform: translateX(-50%)
      translateY(-50%);
    z-index: 1000;

    &__header {
      display: flex;
      justify-content: flex-end;

      .btn-close {
        padding: 0;
        background: inherit;
        border: none;
        cursor: pointer;
        transform: translateX(50%);

        svg {
          fill: #cbdbee;
        }
      }
    }
    &__main {}
    &__footer {
      display: flex;
      justify-content: space-between;
    }

    img {
      width: inherit;
      max-width: calc(100vw - 200px);
      max-height: calc(100vh - 200px);
      height: inherit;
    }
  }
}
</style>
