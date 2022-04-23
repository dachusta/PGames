<template>
  <div>

  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const gameItem = ref([])

async function api () {
  const url = 'https://api.rawg.io/api/games?key=8f4899e2e65a42e58807bc9bbec35cca&page=1&page_size=40'
  const response = await fetch(url)
  const commits = await response.json()
  console.log(commits)
  gameItem.value = commits.results
}
onMounted(api())

</script>

<style lang="scss" scoped>

</style>
