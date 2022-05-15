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
      <!-- <div class="description"> -->
        <p class="description-text">{{ gameItem.description_raw }}</p>
      <!-- </div> -->
    </div>
    <main class="main">
      Buy:
      <div
        class="stores"
        v-for="store in gameStores.results"
        :key="store.id"
      >
        <a :href="store.url">{{ hostName(store.url).hostname }}</a>
      </div>
      Additions:
      <div
        class="additions"
        v-for="addition in gameAdditions.results"
        :key="addition.id"
      >
        {{addition.name}}
        <!-- {{addition.name}} -->
      </div>
      gameSeries:
      <div
        class="series"
        v-for="series in gameSeries.results"
        :key="series.id"
      >
        {{series.name}}
        <!-- {{series.background_image}} -->
      </div>
      gameAchievements:
      <div
        class="achievement"
        v-for="achievement in gameAchievements.results"
        :key="achievement.id"
      >
        {{achievement.name}}
        <!-- {{series.image}} -->
      </div>
      <!-- {{gameAchievements.results}} -->
    </main>
    <div class="right-bar">
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
    "header header header header"
    "screenshots screenshots description description"
    "main main main right-bar"
    "footer footer footer footer";
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
// .description {
  // letter-spacing: 1px;
  // line-height: 1.2;
  // font-size: 16px;
  // white-space: pre-wrap;
// }
.main-img {
  width: 320px;
  height: 180px;
  float: left;
  margin-right: 10px;
}
.description-text {
  line-height: 1.2;
  font-size: 16px;
  white-space: pre-wrap;
  margin: 0;
  overflow: hidden;
  position: relative;
  max-height: 114px;
  // overflow: hidden;
  // text-overflow: ellipsis;
  // display: -webkit-box;
  // -webkit-line-clamp: 7;
  // height: 100%;
  // -webkit-box-orient: vertical;
}
.description-text:after {
  content: "";
  text-align: right;
  position: absolute;
  bottom: 0;
  right: 0;
  left: 0;
  height: 1.2em;
  background: linear-gradient(to bottom, rgba(255, 255, 255, 0), rgba(60, 68, 100, 0.7) 100%);
  pointer-events: none;
}
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
  // width: 100%;
  padding: 20px;
  background: rgba(60, 68, 100, 0.7);
  z-index: 1;
}
.stores a {
  color: inherit;
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
