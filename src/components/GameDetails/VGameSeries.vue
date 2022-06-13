<template>
  <div class="game-series">
    <div class="game-series__title">
      Game series:
    </div>
    <div class="game-series__list">
      <div
        class="game"
        v-for="series in props.list"
        :key="series.id"
      >
        <img
          class="game__img"
          :src="series?.background_image"
          alt="game"
        >
        <div class="game__name">
          {{ series.name }}
        </div>
      </div>
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
.game-series {
  display: grid;
  gap: 10px;
  padding: 15px 30px;
  background: rgba(39, 41, 63, 0.75);

  &__title {
    display: flex;
    justify-self: flex-start;
    padding: 5px 20px;
    font-size: 16px;
    font-weight: 700;
    letter-spacing: 1px;
    background: rgba(102, 204, 51, 0.75);
  }

  &__list {
    display: flex;
    gap: 15px;
    overflow-y: hidden;
  }

  .game {
    display: grid;

    &__img {
      background: rgba(39, 41, 63);
      width: 256px;
      height: 144px;
    }
  }
}
</style>
