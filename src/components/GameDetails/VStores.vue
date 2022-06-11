<template>
  <div class="stores">
    <div class="stores__title">Where to buy:</div>
    <div class="stores__list">
      <a
        :href="store.url"
        class="store"
        v-for="store in props.list"
        :key="store.id"
      >
        <img v-if="storeName(store.url) === 'App Store'" class="store__logo" src="@/assets/stores/appstore.png" alt="">
        <img v-else-if="storeName(store.url) === 'PlayStation'" class="store__logo" src="@/assets/stores/playstation.png" alt="">
        <img v-else-if="storeName(store.url) === 'Microsoft'" class="store__logo" src="@/assets/stores/microsoft.png" alt="">
        <img v-else-if="storeName(store.url) === 'Steam'" class="store__logo" src="@/assets/stores/steam.png" alt="">
        <img v-else-if="storeName(store.url) === 'GOG'" class="store__logo" src="@/assets/stores/gog.png" alt="">
        <img v-else-if="storeName(store.url) === 'Xbox'" class="store__logo" src="@/assets/stores/xbox.png" alt="">
        <img v-else-if="storeName(store.url) === 'Nintendo'" class="store__logo" src="@/assets/stores/nintendo.png" alt="">
        <img v-else-if="storeName(store.url) === 'Google Play'" class="store__logo" src="@/assets/stores/googleplay.png" alt="">
        <img v-else-if="storeName(store.url) === 'Epic Games'" class="store__logo" src="@/assets/stores/epicgames.png" alt="">
        <p class="store__text">{{ storeName(store.url) }}</p>
        <a :href="store.url" class="store__btn">Buy</a>
      </a>
    </div>
  </div>
</template>

<script setup>
// eslint-disable-next-line
const props = defineProps({
  list: Array
})

function storeName (store) {
  const hostname = new URL(store).hostname

  switch (hostname) {
    case 'apps.apple.com':
      return 'App Store'
    case 'store.playstation.com':
      return 'PlayStation'
    case 'www.microsoft.com':
      return 'Microsoft'
    case 'store.steampowered.com':
      return 'Steam'
    case 'www.gog.com':
      return 'GOG'
    case 'marketplace.xbox.com':
      return 'Xbox'
    case 'www.nintendo.com':
      return 'Nintendo'
    case 'play.google.com':
      return 'Google Play'
    case 'www.epicgames.com':
      return 'Epic Games'
    default:
      return 'Some kind of store'
  }
}
</script>

<style lang="scss" scoped>
.stores {
  display: grid;
  align-content: flex-start;
  gap: 10px;
  background: rgba(39, 41, 63, 0.75);
  // height: 145px;

  &__title {
    display: flex;
    justify-self: flex-start;
    padding: 3px 10px;
    font-size: 14px;
    background: rgba(102, 204, 51, 0.75);
  }

  &__list {
    display: grid;
    gap: 10px;
    padding: 10px 20px;
    overflow: auto;

    .store {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 10px 0px 10px 15px;
      background: #3C4464;
      color: inherit;

      &__logo {
        // background: rgba(39, 41, 63);
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
}
</style>
