<template>
<div class="page">
  <TheSidebar
    class="sidebar"
  />
  <div
    class="game-item"
    :style="{ background: `no-repeat center url(${gameItem.background_image}) fixed` }"
    style="background-size: cover;"
  >
    <header class="header">
      <!-- <div class="name">{{ gameItem.name }}</div> -->

      <!-- <div class="rating">
        <div class="name">Rating: {{ gameItem.rating }}</div>
        <div class="name">Metacritic: {{ gameItem.metacritic }}</div>
      </div> -->
    </header>
    <div class="wrap left screenshots-list?">
        <!-- v-for="screenshot in gameScreenshots.results" -->
      <img
        class="screenshots-item"
        :src="gameScreenshots?.results?.[0]?.image"
        alt="1"
      />
    </div>
    <div class="right">
      <div class="container">
        <img class="main-img" :src="gameItem.background_image" alt="">
        <div class="main-info">
          <p class="name">{{ gameItem.name }}</p>
          <p class="name">Rating: {{ gameItem.rating }}</p>
          <p class="name">Metacritic: {{ gameItem.metacritic }}</p>
        </div>
        <!-- gameMovies -->
      </div>
    </div>
    <main class="main">
      <div class="stores">
        <div class="stores__title">
          Where to buy:
        </div>
        <a :href="store.url"
          class="store"
          v-for="store in gameStores.results"
          :key="store.id"
        >
          <div class="store__icon"></div>
          <p class="store__text">{{ hostName(store.url).hostname }}</p>
            <!-- apps.apple.com
            store.playstation.com
            www.microsoft.com
            store.steampowered.com
            www.gog.com
            marketplace.xbox.com
            www.nintendo.com
            play.google.com
            www.epicgames.com -->
          <a :href="store.url" class="store__btn">Buy</a>
        </a>
      </div>
      <div class="description">
        <div class="description__title">
          About
        </div>
        <p class="description__text">{{ gameItem.description_raw }}</p>
      </div>
      <div
        class="additions"
      >
        <div class="additions__title">
          Additions:
        </div>
        <a
          class="addition"
          v-for="addition in gameAdditions.results"
          :key="addition.id"
        >
          <img
            class="addition__img"
            :src="addition?.background_image"
            alt=".img"
          >
          <p class="addition__text">{{ addition.name }}</p>
        </a>
      </div>
      <div class="game-series">
        <div class="game-series__title">
          Game series:
        </div>
        <div class="game-series__list">
          <div
            class="game"
            v-for="series in gameSeries.results"
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
      <div class="achievements">
        <div class="achievements__title">
          Achievements:
        </div>
        <div
          class="achievement"
          v-for="achievement in gameAchievements.results"
          :key="achievement.id"
        >
          <img
            class="achievement__img"
            :src="achievement.image"
            alt=".img"
          >
          <div class="achievement__text">
            <div class="achievement__name">
              {{ achievement.name }}
            </div>
            <div class="achievement__description">
              {{ achievement.description }}
            </div>
          </div>
          <div class="achievement__percent">
            {{ achievement.percent }}
          </div>
        </div>
      </div>
    </main>
    <div v-if="false" class="right-bar">
      <div class="name">Released: {{ gameItem.released }}</div>
      <div class="name">Updated: {{ gameItem?.updated }}</div>
      <div class="name">Esrb rating: {{ gameItem.esrb_rating.name }}</div>
      <!-- <div class="name">{{ gameItem.added }}</div> -->
      <!-- <div class="name">{{ gameItem.added_by_status }}</div> -->
      <!-- <div class="tags">
        tags
        <div
          class="tag"
          v-for="tag in gameItem.tags"
          :key="tag.id"
        >{{ tag.name }}</div>
      </div> -->
      <div class="tags">
        tags
        <div
          class="tag"
          v-for="tag in gameItem.tags"
          :key="tag.id"
        >{{ tag.name }}</div>
      </div>
      <div class="tags">
        genres
        <div
          class="tag"
          v-for="genre in gameItem.genres"
          :key="genre.id"
        >{{ genre.name }}</div>
      </div>
      <!-- <div class="name">Rating: {{ gameItem.rating }}</div>
      <div class="name">Metacritic: {{ gameItem.metacritic }}</div> -->
      <div class="name">Playtime: {{ gameItem.playtime }}</div>
      <div class="tags">
        Stores:
        <div
          class="tag"
          v-for="store in gameItem.stores"
          :key="store.store.id"
        >{{ store.store.name }}</div>
      </div>
      <!-- <div class="name">Stores: {{ gameItem.stores }}</div> -->
      <div class="tags">
        Ratings:
        <div
          class="tag"
          v-for="rating in gameItem.ratings"
          :key="rating.id"
        > =={{ rating.title }} | {{ rating.count }} | {{ rating.percent }}== </div>
      </div>
      <!-- <div class="name">Ratings: {{ gameItem.ratings }}</div> -->
      <div class="tags">
        Developers:
        <div
          class="tag"
          v-for="developer in gameItem.developers"
          :key="developer.id"
        >{{ developer.name }}</div>
      </div>
      <div class="tags">
        Publishers:
        <div
          class="tag"
          v-for="publisher in gameItem.publishers"
          :key="publisher.id"
        >{{ publisher.name }}</div>
      </div>
      <!-- <div class="name">Developers: {{ gameItem.developers }}</div> -->
    </div>
    <footer class="footer">
      <div class="name" :style="{ background: '#'+gameItem.dominant_color }">{{ gameItem.dominant_color }}</div>
      <div class="name">{{ gameItem.background_image }}</div>
    </footer>
  </div>
</div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import TheSidebar from '@/components/TheSidebar.vue'

// const props = defineProps({
//   id: String
// })

const gameItem = ref({})
const gameScreenshots = ref([])
const gameAdditions = ref([])
const gameSeries = ref([])
const gameStores = ref([])
const gameAchievements = ref([])
const gameMovies = ref([])
const route = useRoute()

console.log(route.params.id)

function hostName (store) {
  return new URL(store)
}

async function api (id = 3498) {
  const url = `https://api.rawg.io/api/games/${id}?key=8f4899e2e65a42e58807bc9bbec35cca`
  const response = await fetch(url)
  const commits = await response.json()
  gameItem.value = commits
  console.log('gameItem', gameItem.value.results)
}
async function apiScreenshots (id = 3498) {
  const url = `https://api.rawg.io/api/games/${id}/screenshots?key=8f4899e2e65a42e58807bc9bbec35cca`
  const response = await fetch(url)
  const commits = await response.json()
  gameScreenshots.value = commits
  console.log('screenshots', gameScreenshots.value.results)
}
async function apiAdditions (id = 3498) {
  //  список DLC для игры, GOTY и других выпусков, сопутствующих приложений и т. д.
  const url = `https://api.rawg.io/api/games/${id}/additions?key=8f4899e2e65a42e58807bc9bbec35cca`
  const response = await fetch(url)
  const commits = await response.json()
  gameAdditions.value = commits
  console.log('additions', gameAdditions.value.results)
}
async function apiSeries (id = 3498) {
  //  список игр, которые являются частью той же серии.
  const url = `https://api.rawg.io/api/games/${id}/game-series?key=8f4899e2e65a42e58807bc9bbec35cca`
  const response = await fetch(url)
  const commits = await response.json()
  gameSeries.value = commits
  console.log('game-series', gameSeries.value.results)
}
async function apiStores (id = 3498) {
  //  ссылки на магазины, продающие игру.
  const url = `https://api.rawg.io/api/games/${id}/stores?key=8f4899e2e65a42e58807bc9bbec35cca`
  const response = await fetch(url)
  const commits = await response.json()
  gameStores.value = commits
  console.log('stores', gameStores.value.results)
}
async function apiAchievements (id = 3498) {
  //  список игровых достижений.
  const url = `https://api.rawg.io/api/games/${id}/achievements?key=8f4899e2e65a42e58807bc9bbec35cca`
  const response = await fetch(url)
  const commits = await response.json()
  gameAchievements.value = commits
  console.log('achievements', gameAchievements.value.results)
}
async function apiMovies (id = 3498) {
  //  список игровых трейлеров.
  const url = `https://api.rawg.io/api/games/${id}/movies?key=8f4899e2e65a42e58807bc9bbec35cca`
  const response = await fetch(url)
  const commits = await response.json()
  gameMovies.value = commits
  console.log('movies', gameMovies.value.results)
}

onMounted(
  api(route.params.id),
  apiScreenshots(route.params.id),
  apiAdditions(route.params.id),
  apiSeries(route.params.id),
  apiStores(route.params.id),
  apiAchievements(route.params.id),
  apiMovies(route.params.id)
)

</script>

<style lang="scss" scoped>
.page {
  display: grid;
  grid-template-columns: 250px 1fr;
  background: #1C1C2C;
  color: #CBDBEE;
  position: relative;

}
.game-item {
  display: grid;
  grid-template-areas:
    "header header"
    "screenshots description"
    "main main"
    "footer footer";
  // grid-template-columns: 1fr;
  // grid-template-rows: 1fr;
  gap: 30px;
  // margin-left: 250px;
  padding: 30px;
  // z-index: 0;
}
.page::after {
  content: "";
  background: #1C1C2C;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  opacity: 0.7;
  z-index: 0;
}
.sidebar {
  z-index: 1;
}
// .game-item {
//   z-index: 1;
// }
.header {
  grid-area: header;
  display: flex;
  justify-content: space-between;
  z-index: 1;
}
.name {
  font-size: 24px;
  // padding: 0;
  margin: 0;
}
.main-info {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.left {
  grid-area: screenshots;
  display: flex;
  flex-wrap: wrap;
  background: rgba(60, 68, 100, 0.7);
  z-index: 1;
}
.screenshots-item {
  width: 640px;
  height: 360px;
}
.right {
  grid-area: description;
  display: flex;
  flex-direction: column;
  gap: 20px;
  padding: 20px;
  background: rgba(60, 68, 100, 0.7);
  z-index: 1;
  // max-height: 360px;
}
.container {
  display: flex;
  // justify-content: space-between;
}
.main-img {
  width: 320px;
  height: 180px;
  float: left;
  margin-right: 10px;
}
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
.description {
  // line-height: 1.2;
  // font-size: 16px;
  // white-space: pre-wrap;
  // overflow: hidden;
  // position: relative;
  // max-height: 114px;

}
// .description-text:after {
//   content: "";
//   text-align: right;
//   position: absolute;
//   bottom: 0;
//   right: 0;
//   left: 0;
//   height: 1.2em;
//   background: linear-gradient(to bottom, rgba(255, 255, 255, 0), rgba(60, 68, 100, 0.7) 100%);
//   pointer-events: none;
// }
.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
  margin: 5px;
}
.tag {
  background: #1C1C2C;
  padding: 3px 5px;
}
.main {
  grid-area: main;
  display: grid;
  gap: 10px;
  // width: 100%;
  padding: 20px;
  background: rgba(60, 68, 100, 0.7);
  z-index: 1;
}
.stores {
  display: grid;
  gap: 10px;
  padding: 15px 30px;
  background: rgba(39, 41, 63, 0.75);

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

.additions {
  display: grid;
  gap: 10px;
  padding: 15px 30px;
  background: rgba(39, 41, 63, 0.75);

  &__title {
    display: flex;
    justify-self: flex-start;
    padding: 3px 10px;
    font-size: 14px;
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

.game-series {
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

  &__list {
    display: flex;
    gap: 15px;
    overflow: auto;
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

.achievements {
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

  .achievement {
    display: flex;
    align-items: center;
    gap: 10px;
    background: #3C4464;

    &__img {
      width: 80px;
      height: 80px;
      background: rgba(39, 41, 63);
    }

    &__text {
      flex: 1 1 100%;
    }

    &__name {
      font-size: 16px;
    }

    &__description {
      font-size: 14px;
      color: #8490a9;
    }

    &__percent {
      padding-right: 30px;
    }
  }
}

.right-bar {
  grid-area: right-bar;
  width: 250px;
  padding: 20px;
  background: rgba(60, 68, 100, 0.7);
  z-index: 1;
}
.footer {
  grid-area: footer;
  padding: 20px;
  background: rgba(60, 68, 100, 0.7);
  z-index: 1;
}
</style>
