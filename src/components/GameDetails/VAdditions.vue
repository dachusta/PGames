<template>
  <div class="additions">
    <div class="additions__title">
      Additions:
    </div>
    <a
      v-for="addition in props.list"
      :key="addition.id"
      class="addition"
    >
      <img
        class="addition__img"
        :src="addition?.background_image"
        alt=".img"
      >
      <p class="addition__text">{{ addition.name }}</p>
    </a>
  </div>
</template>

<script setup>
// eslint-disable-next-line
const props = defineProps({
  list: {
    type: Array,
    default: () => []
  }
})

</script>

<style lang="scss" scoped>
.additions {
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

  .addition {
    display: flex;
    align-items: center;
    gap: 10px;
    // padding: 10px 0px 10px 15px;
    background: #3C4464;
    color: inherit;

    &__img {
      background: rgba(39, 41, 63);
      width: 128px;
      height: 72px;
    }

    &__text {
      margin: 0;
      font-size: 16px;
    }
  }
}
</style>
