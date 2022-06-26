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
          <div class="title">
            {{ gameItem.name }}
          </div>
          <!-- <img class="main-img" :src="gameItem.background_image" alt=""> -->
          <VStores
            v-if="gameStores.results?.length"
            class="stores"
            :list="gameStores.results"
          />
          <div class="container--column container--dprug">
            <div class="container--column">
              <div class="developers">
                <div class="developers__title">
                  Developers:
                </div>
                <div
                  v-for="developer in gameItem.developers"
                  :key="developer.id"
                  class="developer"
                >
                  {{ developer.name }}
                </div>
              </div>
              <div class="publishers">
                <div class="publishers__title">
                  Publishers:
                </div>
                <div
                  v-for="publisher in gameItem.publishers"
                  :key="publisher.id"
                  class="publisher"
                >
                  {{ publisher.name }}
                </div>
              </div>
            </div>
            <div class="container--column">
              <div class="released">
                <div class="released__title">
                  Released:
                </div>
                <div class="released__date">
                  {{ released }}
                </div>
              </div>
              <div class="updated">
                <div class="updated__title">
                  Updated:
                </div>
                <div class="updated__date">
                  {{ updated }}
                </div>
              </div>
            </div>
            <div class="genres">
              <div class="genres__title">
                Genres:
              </div>
              <div
                v-for="genre in gameItem.genres"
                :key="genre.id"
                class="genre"
              >
                {{ genre.name }}
              </div>
            </div>
          </div>
          <div class="container container--rating">
            <!-- circular progress bar -->
            <div
              v-if="ratingPercent"
              class="rating"
            >
              <div
                class="percent"
                :style="{'--clr':'#04fc43', '--num': ratingPercent}"
              >
                <div class="dot" />
                <svg>
                  <circle
                    cx="50"
                    cy="50"
                    r="50"
                  />
                  <circle
                    cx="50"
                    cy="50"
                    r="50"
                  />
                </svg>
                <div class="number">
                  <h2>{{ ratingPercent }}</h2>
                  <p>Rating</p>
                </div>
              </div>
            </div>
            <div
              v-if="gameItem.metacritic"
              class="metacritic"
            >
              <div
                class="percent"
                :style="{'--clr':'#04fc43', '--num': gameItem.metacritic}"
              >
                <div class="dot" />
                <svg>
                  <circle
                    cx="50"
                    cy="50"
                    r="50"
                  />
                  <circle
                    cx="50"
                    cy="50"
                    r="50"
                  />
                </svg>
                <div class="number">
                  <h2>{{ gameItem.metacritic }}</h2>
                  <p>Metacritic</p>
                </div>
              </div>
            </div>
            <div
              v-if="gameItem.esrb_rating?.name"
              class="esrb-rating"
            >
              <img
                :src="require(`@/assets/esrb/${gameItem.esrb_rating?.name}.png`)"
                alt=""
              >
            </div>
            <div
              v-if="gameItem.playtime"
              class="playtime"
            >
              <IconTimer :time="gameItem.playtime" />
            </div>
          </div>
          <div class="tags">
            <div class="tags__title">
              Tags:
            </div>
            <div
              v-for="tag in gameItem.tags"
              :key="tag.id"
              class="tag"
            >
              {{ tag.name }}
            </div>
          </div>
        </div>
        <div class="additional">
          <VDescription
            v-if="gameItem.description_raw?.length"
            class="description"
            :text="gameItem.description_raw"
          />
          <VAdditions
            v-if="gameAdditions.results?.length"
            class="additions"
            :list="gameAdditions.results"
          />
          <VGameSeries
            v-if="gameSeries.results?.length"
            class="game-series"
            :list="gameSeries.results"
          />
          <VAchievements
            v-if="gameAchievements.results?.length"
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
import { ref, computed, watch } from 'vue'
import { useRoute } from 'vue-router'
import TheSidebar from '@/components/TheSidebar.vue'
import VScreenshots from '@/components/GameDetails/VScreenshots.vue'
import VStores from '@/components/GameDetails/VStores.vue'
import VDescription from '@/components/GameDetails/VDescription.vue'
import VAdditions from '@/components/GameDetails/VAdditions.vue'
import VGameSeries from '@/components/GameDetails/VGameSeries.vue'
import VAchievements from '@/components/GameDetails/VAchievements.vue'
import IconTimer from '@/components/icons/IconTimer.vue'

// const props = defineProps({
//   id: String
// })

const ratingPercent = computed(() => Math.round((100 / 5) * gameItem.value.rating))
watch(() => ratingPercent, (first) => {
  console.log(first)
})
const gameItem = ref({})
const gameScreenshots = ref([])
const gameAdditions = ref([])
const gameSeries = ref([])
const gameStores = ref([])
const gameAchievements = ref([])
const gameMovies = ref([])
const route = useRoute()

function dtFormat (date) {
  const handler = (d) => d < 10 ? '0' + d : d

  date = new Date(date)
  const year = date.getFullYear()
  const month = handler(date.getMonth() + 1)
  const day = handler(date.getDate())

  return day + '.' + month + '.' + year
}
const released = computed(() => dtFormat(gameItem.value.released))
const updated = computed(() => dtFormat(gameItem.value.updated))

console.log(route.params.id)

async function api (id = 3498) {
  const url = `https://api.rawg.io/api/games/${id}?key=8f4899e2e65a42e58807bc9bbec35cca`
  const response = await fetch(url)
  const commits = await response.json()
  gameItem.value = commits
  console.log('gameItem', gameItem.value)
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

watch(
  () => route.params.id,
  () => {
    api(route.params.id)
    apiScreenshots(route.params.id)
    apiAdditions(route.params.id)
    apiSeries(route.params.id)
    apiStores(route.params.id)
    apiAchievements(route.params.id)
    apiMovies(route.params.id)

    window.scrollTo(0, 0)
  },
  { deep: true }
)

// onMounted(
api(route.params.id)
apiScreenshots(route.params.id)
apiAdditions(route.params.id)
apiSeries(route.params.id)
apiStores(route.params.id)
apiAchievements(route.params.id)
apiMovies(route.params.id)
// )

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
  position: relative;
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
      max-height: 368px;
    }

    .container--dprug {
      grid-area: dprug;
      justify-content: space-between;
    }

    .container--rating {
      grid-area: rating;
      position: relative;
      display: flex;
      align-content: flex-start;
      justify-content: flex-end;
      flex-wrap: wrap;
      max-width: 250px;
      gap: 10px;

      > div {
        position: relative;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 120px;
        height: 120px;
        // background: rgba(39, 41, 63, 0.75);
      }

      .rating .percent, .metacritic .percent {
        position: relative;
        width: 110px;
        height: 110px;
        // background: red;

        .dot {
          position: absolute;
          inset: 5px;
          z-index: 10;
          transform: rotate(calc(3.6deg * var(--num)));
          /* 360deg / 100 = 3.6 */

          animation: animateDot 2s linear forwards;

          @keyframes animateDot {
            0% {
              transform: rotate(0deg);
            }
            100% {
              transform:  rotate(calc(3.6deg * var(--num)));
            }
          }

          &::before {
            content: '';
            position: absolute;
            top: -7.5px;
            left: 50%;
            transform: translateX(-50%);
            width: 15px;
            height: 15px;
            border-radius: 50%;
            background: var(--clr);
            box-shadow:  0 0 15px var(--clr),
            0 0 45px var(--clr);
          }
        }

        svg {
          position: relative;
          width: 110px;
          height: 110px;
          transform: rotate(270deg);

          circle {
            width: 100%;
            height: 100%;
            fill: transparent;
            stroke-width: 5;
            stroke: rgba(39, 41, 63, 0.75);
            transform: translate(5px, 5px);

            &:nth-child(2) {
              stroke: var(--clr);
              // Math.PI * (d || (r*2))
              stroke-dasharray: 314;
              stroke-dashoffset: calc(314 - (314 * var(--num)) / 100);

              opacity: 0;
              animation: fadeIn 1s linear forwards;
              animation-delay: 2.5s;
            }

            @keyframes fadeIn {
              0% {
                opacity: 0;
                fill: transparent;
              }
              100% {
                opacity: 1;
                fill: rgba(39, 41, 63, 0.75);
              }
            }
          }
        }

        .number {
          position: absolute;
          inset: 0;
          display: flex;
          justify-content: center;
          align-items: center;
          flex-direction: column;

          opacity: 0;
          animation: fadeIn 1s linear forwards;
          animation-delay: 2.5s;
        }

        h2 {
          display: flex;
          justify-content: center;
          align-items: center;
          margin: 0;
        }

        p {
          margin: 0;
        }
      }
    }

    .tags {
      grid-area: tags;
      // max-height: 202px;
      max-height: 88px;
      overflow: hidden;
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

.developers, .publishers, .genres, .released, .updated, .tags {
  display: flex;
  flex-wrap: wrap;
  align-content: flex-start;
  align-items: center;
  gap: 5px;

  &__title {
    flex: 0 0 90px;
    font-size: 15px;
    font-weight: 500;
    color: rgba(203, 219, 238, 65%);
  }
}
.developer, .publisher, .genre, .tag {
  background: #1C1C2C;
  padding: 3px 5px;
}

.footer {
  grid-area: footer;
  padding: 20px;
  background: rgba(60, 68, 100, 0.7);
  // z-index: 1;
}
</style>
