<template>
  <div>
    <div class="name">{{ gameItem.name }}</div>
    <div class="name">{{ gameItem.description }}</div>
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
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'

// const props = defineProps({
//   id: String
// })

const gameItem = ref({})
const route = useRoute()

console.log(route.params.id)

async function api (id) {
  const url = `https://api.rawg.io/api/games/${id}?key=8f4899e2e65a42e58807bc9bbec35cca`
  const response = await fetch(url)
  const commits = await response.json()
  console.log(commits)
  gameItem.value = commits
}
onMounted(api(route.params.id))

</script>

<style lang="scss" scoped>

</style>
