<template>
  <div class="content">
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
          <div class="search">
            <input type="text">
          </div>
          <div class="sort">
            <select name="" id="">
              <option value="">1</option>
              <option value="">2</option>
              <option value="">3</option>
            </select>
          </div>
          <div class="display-mode"></div>
        </div>
      </header>
      <main class="main">
        <div
          class="game-item"
          v-for="game in gameList"
          :key="game.id"
        >
          <!-- <img :src="game.background_image" alt=""> -->
          <img :src="game.short_screenshots[0].image" alt="">
          <div class="row">
            <span class="name">{{ game.name }}</span>
            <span
              class="rating"
              :style="{ background: ratingBG(game.rating) }"
            >{{ game.rating }}</span>
          </div>
          <div class="description"></div>
          <div class="platform-list">
            <span
              class="platform-item"
              v-for="platform in game.parent_platforms"
              :key="platform"
            >
              {{ platform.platform.name }}
            </span>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script setup>
// import { ref, onMounted, watch, toRefs, computed, method } from 'vue'
import { ref, onMounted } from 'vue'

const gameList = ref([])
// const repositoriesMatchingSearchQuery = computed(() => {
//   return repositories.value.filter(
//     repository => repository.name.includes(searchQuery.value)
//   )
// })
function ratingBG (params) {
  if (params > 4) {
    return 'green'
  } else if (params > 3) {
    return 'yellow'
  } else {
    return 'red'
  }
}

async function api () {
  const url = 'https://api.rawg.io/api/games?key=8f4899e2e65a42e58807bc9bbec35cca&page=1&page_size=40'
  const response = await fetch(url)
  const commits = await response.json()
  console.log(commits)
  gameList.value = commits.results
}
onMounted(api())

</script>

<style lang="scss" scoped>
.content {
  display: grid;
  grid-template-columns: 250px 1fr;
  color: #CBDBEE;
}
.sidebar {
  background: #27293F;
  padding: 10px;
  .logo {
    position: sticky;
    top: 10px;
  }
  .nav {
    position: sticky;
    top: 28px;
  }
}
.page {
  background: #1C1C2C;
  padding: 30px;
}
.header {
  height: 160px;
}
.main {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  gap: 30px;
}
@media (max-width: 1655px) {
  .main {
    grid-template-columns: 1fr 1fr 1fr;
    gap: 30px;
  }
}
.game-item {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  background: #3C4464;
  gap: 5px;
}
.game-item img {
  width: 100%;
  height: calc(100% - 95px);
  object-fit: cover;
}
.row {
  display: flex;
  justify-content: space-between;
  padding: 0px 5px;
}
.game-item .name {
  font-size: 18px;
}
.game-item .rating {
  font-size: 14px;
  background: #000;
  color: #000;
  padding: 5px;
  align-self: flex-start;
  // text-shadow: #000 0px 0px 2px;
}
.platform-list {
  display: flex;
  justify-content: flex-end;
  flex-wrap: wrap;
  gap: 5px;
  margin: 5px;
  align-self: flex-end;
}
.platform-item {
  display: block;
  font-size: 14px;
  padding: 3px 5px 3px 5px;
  background: #1C1C2C;
  border-radius: 5px;
}

</style>
