<template>
  <div class="description">
    <div class="description__title">
      About
    </div>
    <p class="description__text">{{ props.text }}</p>
  </div>
</template>

<script setup>
// eslint-disable-next-line
const props = defineProps({
  text: String
})

</script>

<style lang="scss" scoped>
.description {
  display: grid;
  gap: 10px;
  padding: 15px 30px;
  background: rgba(39, 41, 63, 0.75);

  &__title {
    display: flex;
    padding: 3px 10px;
    justify-self: flex-start;
    font-size: 14px;
    background: rgba(102, 204, 51, 0.75);
  }

  &__text {
    margin: 0;
    white-space: pre-wrap;
  }
}
</style>
