<template>
<div class="wrapper">
  <TheSidebar
    class="sidebar"
  />
  <div
    class="page"
    :style="{ background: `no-repeat center url(${gameItem.background_image}) fixed` }"
    style="background-size: cover;"
  >
    <header class="header">
      search
    </header>
    <main class="main">
      <VScreenshots
        class="screenshots"
        :list="gameScreenshots.results"
      />
      <!-- company -->
      <div class="details">
        <div class="title">{{ gameItem.name }}</div>
        <!-- <img class="main-img" :src="gameItem.background_image" alt=""> -->
        <VStores
          class="stores"
          :list="gameStores.results"
        />
        <div class="container--column container--dprug">
          <div class="developers">
            Developers:
            <div
              class="developer"
              v-for="developer in gameItem.developers"
              :key="developer.id"
            >{{ developer.name }}</div>
          </div>
          <div class="publishers">
            Publishers:
            <div
              class="publisher"
              v-for="publisher in gameItem.publishers"
              :key="publisher.id"
            >{{ publisher.name }}</div>
          </div>
          <div class="released">Released: {{ gameItem.released }}</div>
          <div class="updated">Updated: {{ gameItem?.updated }}</div>
          <div class="genres">
            Genres:
            <div
              class="genre"
              v-for="genre in gameItem.genres"
              :key="genre.id"
            >{{ genre.name }}</div>
          </div>
        </div>
        <div class="container container--rating">
          <div class="rating">Rating: {{ gameItem.rating }}</div>
          <div class="metacritic">Metacritic: {{ gameItem.metacritic }}</div>
          <div class="name-">Esrb rating: {{ gameItem.esrb_rating.name }}</div>
          <div class="name-">Playtime: {{ gameItem.playtime }}</div>
        </div>
        <div class="tags">
          Tags
          <div
            class="tag"
            v-for="tag in gameItem.tags"
            :key="tag.id"
          >{{ tag.name }}</div>
        </div>
      </div>
      <div class="additional">
        <VDescription
          class="description"
          :text="gameItem.description_raw"
        />
        <VAdditions
          class="additions"
          :list="gameAdditions.results"
        />
        <VGameSeries
          class="game-series"
          :list="gameSeries.results"
        />
        <VAchievements
          class="achievements"
          :list="gameAchievements.results"
        />
      </div>
    </main>
    <footer class="footer">
      <!-- <div class="name">{{ gameItem.added }}</div> -->
      <!-- <div class="name">{{ gameItem.added_by_status }}</div> -->
      Made with love
    </footer>
  </div>
</div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import TheSidebar from '@/components/TheSidebar.vue'
import VScreenshots from '@/components/GameDetails/VScreenshots.vue'
import VStores from '@/components/GameDetails/VStores.vue'
import VDescription from '@/components/GameDetails/VDescription.vue'
import VAdditions from '@/components/GameDetails/VAdditions.vue'
import VGameSeries from '@/components/GameDetails/VGameSeries.vue'
import VAchievements from '@/components/GameDetails/VAchievements.vue'

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
  grid-template-areas:
    "header"
    "main"
    "footer";
  gap: 30px;
  padding: 30px;
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
.header {
  grid-area: header;
  display: flex;
  justify-content: space-between;
  z-index: 1;
}
.main {
  grid-area: main;
  display: grid;
  grid-template-areas:
    "screenshots details"
    "additional additional";
  grid-template-columns: 640px 1fr;
  gap: 10px;
  z-index: 1;

  .screenshots {
    grid-area: screenshots;
    width: 640px;
  }

  .details {
    grid-area: details;
    display: grid;
    grid-template-areas:
      "title title title"
      "stores dprug rating"
      "stores tags tags";
    grid-template-columns: 320px 1fr;
    grid-template-rows: max-content;
    gap: 20px;
    padding: 20px;
    background: rgba(60, 68, 100, 0.7);

    .title {
      grid-area: title;
      font-size: 24px;
      margin: 0;
    }

    .stores {
      grid-area: stores;
    }

    .container--dprug {
      grid-area: dprug;
    }

    .container--rating {
      grid-area: rating;
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      max-width: 250px;

      > div {
        width: 120px;
        height: 120px;
        background: rgba(39, 41, 63, 0.75);
      }
    }

    .tags {
      grid-area: tags;
    }
  }

  .additional {
    grid-area: additional;
    display: grid;
    gap: 10px;
    background: rgba(60, 68, 100, 0.7);
  }
}

.container--column {
  display: flex;
  flex-direction: column;
  gap: 5px;
}
// .main-img {
//   width: 320px;
//   height: 180px;
//   float: left;
//   margin-right: 10px;
// }

.developers, .publishers, .genres, .tags {
  display: flex;
  flex-wrap: wrap;
  align-content: flex-start;
  gap: 5px;
}
.developer, .publisher, .genre, .tag {
  background: #1C1C2C;
  padding: 3px 5px;
}

.footer {
  grid-area: footer;
  padding: 20px;
  background: rgba(60, 68, 100, 0.7);
  z-index: 1;
}
</style>
