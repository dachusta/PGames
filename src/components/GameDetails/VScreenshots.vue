<template>
  <div class="screenshots">
    <!-- v-for="screenshot in gameScreenshots.results" -->
    <img
      class="screenshots__display"
      :src="props?.list?.[0]?.image"
      alt="1"
    />
    <div class="screenshots__list">
      <img
        class="screenshots__item"
        v-for="screenshot in props.list"
        :key="screenshot.id"
        :src="screenshot.image"
        :alt="screenshot.id"
      />
    </div>
  </div>
</template>

<script setup>
// eslint-disable-next-line
const props = defineProps({
  list: Array
})
</script>

<style lang="scss" scoped>
.screenshots {
    background: rgba(60, 68, 100, 0.7);

    &__display {
      width: 640px;
      height: 360px;
    }

    &__list {
      display: flex;
      gap: 5px;
      overflow: auto;
    }

    &__item {
      width: 128px;
      height: 72px;
    }
  }
</style>
