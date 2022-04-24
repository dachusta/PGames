<template>
  <div
    class="page game-item"
    :style="{ background: `no-repeat center url(${gameItem.background_image}) fixed` }"
    style="background-size: cover;"
  >
    <header class="header">
      <div class="name">{{ gameItem.name }}</div>
    </header>
    <div class="wrap left screenshots-list?">
        <!-- v-for="screenshot in gameScreenshots.results" -->
      <img
        class="screenshots-item"
        :src="gameScreenshots?.results[0]?.image"
        alt="1"
      />
    </div>
    <div class="right">
      <div class="description">{{ gameItem.description_raw }}</div>
      <div class="name">Released: {{ gameItem.released }}</div>
      <div class="name">Updated: {{ gameItem.updated }}</div>
      <div class="name">Esrb rating: {{ gameItem.esrb_rating.name }}</div>
      <!-- <div class="name">{{ gameItem.added }}</div> -->
      <!-- <div class="name">{{ gameItem.added_by_status }}</div> -->
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
    </div>
    <div class="details">
      <div class="name" :style="{ background: '#'+gameItem.dominant_color }">{{ gameItem.dominant_color }}</div>
      <div class="name">{{ gameItem.metacritic }}</div>
      <div class="name">{{ gameItem.playtime }}</div>
      <div class="name">{{ gameItem.stores }}</div>
      <div class="name">{{ gameItem.ratings }}</div>
      <div class="name">{{ gameItem.developers }}</div>
      <!-- <div class="name">{{ gameItem.background_image }}</div> -->
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'

// const props = defineProps({
//   id: String
// })

const gameItem = ref({})
const gameScreenshots = ref([])
const route = useRoute()

console.log(route.params.id)

async function api (id = 3498) {
  const url = `https://api.rawg.io/api/games/${id}?key=8f4899e2e65a42e58807bc9bbec35cca`
  const response = await fetch(url)
  const commits = await response.json()
  console.log(commits)
  gameItem.value = commits
}
async function apiScreenshots (id = 3498) {
  const url = `https://api.rawg.io/api/games/${id}/screenshots?key=8f4899e2e65a42e58807bc9bbec35cca`
  const response = await fetch(url)
  const commits = await response.json()
  console.log(commits)
  gameScreenshots.value = commits

  console.log(gameScreenshots.value.results)
}
onMounted(api(route.params.id), apiScreenshots(route.params.id))

</script>

<style lang="scss" scoped>
.page {
  display: grid;
  grid-template-areas:
    "header header"
    "screenshots description"
    "details details";
  grid-template-columns: 1fr;
  grid-template-rows: 1fr;
  gap: 30px;
  padding: 10px;
  background: #1C1C2C;
  color: #CBDBEE;
  position: relative;
  z-index: 0;
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
  z-index: 1;
}
.left {
  display: flex;
  flex-wrap: wrap;
  grid-area: screenshots;
  z-index: 1;
}
.screenshots-item {
  width: 640px;
  height: 360px;
}
.right {
  grid-area: description;
  padding: 20px;
  background: rgba(60, 68, 100, 0.7);
  z-index: 1;
}
.name {
  font-size: 24px;
}
.description {
  // letter-spacing: 1px;
  line-height: 1.2;
  font-size: 14px;
  white-space: pre-wrap;
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
.details {
  grid-area: details;
}
</style>
