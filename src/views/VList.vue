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
            <input type="text" />
          </div>
          <div class="sort">
            <select name id>
              <option value>1</option>
              <option value>2</option>
              <option value>3</option>
            </select>
          </div>
          <div class="display-mode"></div>
        </div>
      </header>
      <main class="main">
        <GameItem
          class="card game-item"
          v-for="game in gameList"
          :key="game.id"
          @click="toGameItem(game.id)"

          :screenshots="game.short_screenshots"
          :name="game.name"
          :rating="game.rating"
          :platforms="game.parent_platforms"
        />
      </main>
    </div>
  </div>
</template>

<script setup>
// import { ref, onMounted, watch, toRefs, computed, method } from 'vue'
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import GameItem from '@/components/GameItem.vue'

// const emit = defineEmits(['change', 'delete'])

const router = useRouter()

const gameList = ref([])
// const repositoriesMatchingSearchQuery = computed(() => {
//   return repositories.value.filter(
//     repository => repository.name.includes(searchQuery.value)
//   )
// })

async function api () {
  const url =
    'https://api.rawg.io/api/games?key=8f4899e2e65a42e58807bc9bbec35cca&page=1&page_size=40'
  const response = await fetch(url)
  const commits = await response.json()
  console.log(commits)
  gameList.value = commits.results
}
onMounted(api())

function toGameItem (id) {
  router.push({ name: 'VItem', params: { id: id } })
}
</script>

<style lang="scss" scoped>
.content {
  display: grid;
  grid-template-columns: 250px 1fr;
  color: #cbdbee;
}
.sidebar {
  background: #27293f;
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
  background: #1c1c2c;
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

</style>
