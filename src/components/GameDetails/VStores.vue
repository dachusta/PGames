<template>
  <!-- apps.apple.com
                store.playstation.com
                www.microsoft.com
                store.steampowered.com
                www.gog.com
                marketplace.xbox.com
                www.nintendo.com
                play.google.com
                www.epicgames.com -->
  <div class="stores">
    <div class="stores__title">Where to buy:</div>
    <a
      :href="store.url"
      class="store"
      v-for="store in props.list"
      :key="store.id"
    >
      <div class="store__icon"></div>
      <p class="store__text">{{ hostName(store.url).hostname }}</p>
      <a :href="store.url" class="store__btn">Buy</a>
    </a>
  </div>
</template>

<script setup>
// eslint-disable-next-line
const props = defineProps({
  list: Array
})

function hostName (store) {
  return new URL(store)
}
</script>

<style lang="scss" scoped>
.stores {
  display: grid;
  gap: 10px;
  padding: 10px 20px;
  background: rgba(39, 41, 63, 0.75);
  overflow: auto;
  // height: 145px;

  &__title {
    display: flex;
    justify-self: flex-start;
    padding: 3px 10px;
    font-size: 14px;
    background: rgba(102, 204, 51, 0.75);
  }

  .store {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px 0px 10px 15px;
    background: #3C4464;
    color: inherit;

    &__icon {
      background: rgba(39, 41, 63);
      width: 18px;
      height: 18px;
    }

    &__text {
      margin: 0;
      font-size: 14px;
    }

    &__btn {
      margin-left: auto;
      padding: 3px 10px;
      font-size: 12px;
      background: rgba(102, 204, 51, 0.75);
      color: inherit;
    }
  }
}
</style>
