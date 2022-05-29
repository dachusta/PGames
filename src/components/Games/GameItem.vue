<template>
  <div class="card game-item">
    <!-- <img :src="game.background_image" alt=""> -->
    <div class="card-top">
      <div class="wrap-img">
        <img :src="props.screenshots[0].image" alt />
      </div>
      <div class="row">
        <span class="name">{{ props.name }}</span>
        <span class="rating" :style="{ background: ratingBG(props.rating) }">
          {{
          props.rating
          }}
        </span>
      </div>
    </div>
    <!-- <div class="description"></div> -->
    <div class="platform-list">
      <span
        class="platform-item"
        v-for="platform in props.platforms"
        :key="platform"
      >{{ platform.platform.name }}</span>
    </div>
  </div>
</template>

<script setup>
// eslint-disable-next-line
const props = defineProps({
  screenshots: String,
  name: String,
  rating: String,
  platforms: String
})

function ratingBG (params) {
  if (params > 4) {
    return 'rgb(50 255 50 / 70%)'
  } else if (params > 3) {
    return 'rgb(255 255 50 / 70%)'
  } else {
    return 'rgb(255 50 50 / 70%)'
  }
}
</script>

<style lang="scss" scoped>
.game-item {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 300px;
  background: #3c4464;
  gap: 5px;
  border-radius: 10px;
}
.game-item .card-top {
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
  background: #1c1c2c;
  border-radius: 5px;
}
</style>
