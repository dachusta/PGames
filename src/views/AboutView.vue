<template>
  <div>
    <div class="sidebar">
      <div class="logo">PGames</div>
      <nav class="nav">
        <div class="link">Home</div>
        <div class="link">List</div>
        <div class="link">Top</div>
        <div class="link">4</div>
        <div class="link">5</div>
      </nav>
    </div>
    <div class="page">
      <header class="header">
        <div class="title"></div>
        <div class="control-bar">
          <div class="search"></div>
          <div class="sort"></div>
          <div class="display-mode"></div>
        </div>
      </header>
      <main class="main">
        <div class="game-item">
          <img src="" alt="">
          <div class="name"></div>
          <div class="description"></div>
        </div>
      </main>
    </div>
  </div>
</template>

<script setup>
// import { ref, onMounted, watch, toRefs, computed, method } from 'vue'
import { onMounted } from 'vue'

// const repositoriesMatchingSearchQuery = computed(() => {
//   return repositories.value.filter(
//     repository => repository.name.includes(searchQuery.value)
//   )
// })

async function api () {
  const url = 'https://api.rawg.io/api/games?key=8f4899e2e65a42e58807bc9bbec35cca&page=1&page_size=40'
  const response = await fetch(url)
  const commits = await response.json()
  console.log(commits)
  return commits
}
onMounted(api)

</script>

<style lang="scss" scoped>

</style>
