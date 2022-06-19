<template>
  <div class="stores">
    <div class="stores__title">
      Where to buy:
    </div>
    <div class="stores__list">
      <a
        v-for="store in props.list"
        :key="store.id"
        :href="store.url"
        class="store"
      >
        <img
          class="store__logo"
          :src="require(`@/assets/stores/${fileName(store.url)}`)"
          :alt="fileName(store.url)"
        >
        <p class="store__text">{{ storeName(store.url) }}</p>
        <a
          class="store__btn"
          :href="store.url"
        >Buy</a>
      </a>
    </div>
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

function fileName (store) {
  const hostname = new URL(store).hostname

  switch (hostname) {
    case 'apps.apple.com':
      return 'appstore.png'
    case 'store.playstation.com':
      return 'playstation.png'
    case 'www.microsoft.com':
      return 'microsoft.png'
    case 'store.steampowered.com':
      return 'steam.png'
    case 'www.gog.com':
      return 'gog.png'
    case 'marketplace.xbox.com':
      return 'xbox.png'
    case 'www.nintendo.com':
      return 'nintendo.png'
    case 'play.google.com':
      return 'googleplay.png'
    case 'www.epicgames.com':
      return 'epicgames.png'
  }
}

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
    padding: 5px 20px;
    font-size: 16px;
    font-weight: 700;
    letter-spacing: 1px;
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
      padding: 0px 0px 0px 15px;
      background: #3c4464;
      color: inherit;
      text-decoration: none;

      transition: transform .15s ease, box-shadow .2s ease;

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
        padding: 10px 10px;
        font-size: 12px;
        font-weight: 500;
        letter-spacing: 1px;
        background: rgba(102, 204, 51, 0.75);
        color: inherit;
        text-decoration: none;
      }

      &:hover {
        transform: scale(101%);
        box-shadow: 0px 0px 5px 1px rgba(99, 163, 236, 0.75);
      }

      &:focus {
        transform: scale(100%);
        box-shadow: 0px 0px 5px 1px rgba(99, 163, 236, 0.50);
      }
    }
  }
}
</style>
