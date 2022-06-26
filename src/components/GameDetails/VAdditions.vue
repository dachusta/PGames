<template>
  <div class="additions">
    <div class="additions__title">
      Additions:
    </div>
    <a
      v-for="addition in props.list"
      :key="addition.id"
      class="addition"
      @click="toGameDetails(addition.id)"
    >
      <img
        class="addition__img"
        :src="addition?.background_image"
        alt=".img"
      >
      <p class="addition__name">{{ addition.name }}</p>
      <!-- <div class="addition__date">
        <p class="addition__released">Released: {{ dtFormat(addition.released) }}</p>
        <p class="addition__updated">Updated: {{ dtFormat(addition.updated) }}</p>
      </div>
      <div class="addition__goto">Go to details</div> -->
    </a>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'

// eslint-disable-next-line
const props = defineProps({
  list: {
    type: Array,
    default: () => []
  }
})
const router = useRouter()
function toGameDetails (id) {
  // params -> query
  router.push({ name: 'GameDetails', params: { id } })
  // window.location.reload()
}

// const dtFormat = (date) => {
//   const handler = (d) => d < 10 ? '0' + d : d

//   date = new Date(date)
//   const year = date.getFullYear()
//   const month = handler(date.getMonth() + 1)
//   const day = handler(date.getDate())

//   return day + '.' + month + '.' + year
// }
</script>

<style lang="scss" scoped>
.additions {
  display: grid;
  gap: 10px;
  padding: 15px 30px;
  background: rgba(39, 41, 63, 0.75);

  &__title {
    display: flex;
    justify-self: flex-start;
    padding: 5px 20px;
    font-size: 16px;
    font-weight: 700;
    letter-spacing: 1px;
    background: rgba(102, 204, 51, 0.75);
  }

  .addition {
    display: flex;
    align-items: center;
    gap: 10px;
    // padding: 10px 0px 10px 15px;
    background: #3C4464;
    color: inherit;
    cursor: pointer;
    transition: transform 0.15s ease, box-shadow 0.2s ease;

    &:hover {
      transform: scale(100.1%);
      box-shadow: 0px 0px 10px 1px rgba(99, 163, 236, 75%);
    }

    &__img {
      background: rgba(39, 41, 63);
      width: 128px;
      height: 72px;
    }

    &__name {
      margin: 0;
      font-size: 22px;
      font-weight: 500;
    }

    &__date {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      gap: 10px;
      margin-left: auto;
    }

    &__goto {
      padding: 0 30px 0px 70px;
      font-size: 36px;
      font-weight: 700;
    }
  }
}
</style>
