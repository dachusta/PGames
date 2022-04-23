<template>
  <div class="page game-item">
    <div class="wrap right screenshots-list?">
      <img
        class="screenshots-item"
        v-for="screenshot in gameScreenshots.results"
        :key="screenshot.id"
        :src="screenshot.image"
        alt="1"
      />
    </div>
    <div class="left">
      <div class="name">{{ gameItem.name }}</div>
      <div class="description">{{ gameItem.description_raw }}</div>
    </div>
    <div class="details">
      <div class="name" :style="{ background: '#'+gameItem.dominant_color }">{{ gameItem.dominant_color }}</div>
      <div class="name">{{ gameItem.playtime }}</div>
      <div class="name">{{ gameItem.released }}</div>
      <div class="name">{{ gameItem.metacritic }}</div>
      <div class="name">{{ gameItem.esrb_rating }}</div>
      <div class="name">{{ gameItem.background_image }}</div>
      <div class="name">{{ gameItem.added }}</div>
      <div class="name">{{ gameItem.added_by_status }}</div>
      <div class="name">{{ gameItem.tags }}</div>
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
.game-item {
  display: grid;
  grid-template-areas:
    "screenshots description"
    "details details";
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 30px;
  background: #1C1C2C;
  color: #CBDBEE;
}
.right {
  display: flex;
  flex-wrap: wrap;
  grid-area: screenshots;
}
.screenshots-item {
  width: 250px;
  height: 130px;
}
.left {
  grid-area: description;
  padding: 10px 20px;
  background: #3C4464;
}
.name {
  font-size: 18px;
}
.description {
  font-size: 14px;
  white-space: pre-wrap;
}
.details {
  grid-area: details;
}
</style>
