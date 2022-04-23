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
          class="card game-item"
          v-for="game in gameList"
          :key="game.id"
          @click="gameItem(game.id)"
        >
          <!-- <img :src="game.background_image" alt=""> -->
          <div class="card-top">

            <div class="wrap-img">
              <img :src="game.short_screenshots[0].image" alt="">
            </div>
            <div class="row">
              <span class="name">{{ game.name }}</span>
              <span
                class="rating"
                :style="{ background: ratingBG(game.rating) }"
              >{{ game.rating }}</span>
            </div>
          </div>
          <!-- <div class="description"></div> -->
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
import { useRouter } from 'vue-router'

const router = useRouter()

const gameList = ref([])
// const repositoriesMatchingSearchQuery = computed(() => {
//   return repositories.value.filter(
//     repository => repository.name.includes(searchQuery.value)
//   )
// })
function ratingBG (params) {
  if (params > 4) {
    return 'rgb(50 255 50 / 70%)'
  } else if (params > 3) {
    return 'rgb(255 255 50 / 70%)'
  } else {
    return 'rgb(255 50 50 / 70%)'
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

function gameItem (id) {
  router.push({ name: 'VItem', params: { id: id } })
}

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
  height: 300px;
  background: #3C4464;
  gap: 5px;
  border-radius: 10px;
}
.game-item  .card-top {
 display: flex;
 flex-direction: column;
 gap: 10px;
}
.game-item .wrap-img {
  width: 100%;
  height: 175px;
}
.game-item img {
  width: 100%;
  height: 100%;
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
  font-size: 12px;
  background: #1c1c2c;
  color: #1c1c2c;
  padding: 3px 5px;
  border-radius: 5px;
  font-weight: 700;
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
