<template>
  <div class="sidebar">
    <div class="logo">PGames</div>
    <nav class="nav">
      <!-- <div class="link">Home</div> -->
      <!-- <router-link class="link" to="/">Home</router-link> -->
      <router-link class="link" to="/v-list">List</router-link>
      <router-link class="link" to="/v-item">Item</router-link>
      <div class="link">Top</div>
      <div class="link">4</div>
      <div class="link">5</div>
    </nav>
  </div>
</template>

<script setup>
</script>

<style lang="scss" scoped>
.sidebar {
  background: #27293f;
  padding: 10px;
  .logo {
    position: sticky;
    top: 10px;
  }
  .nav {
    display: flex;
    flex-direction: column;
    position: sticky;
    top: 28px;
  }
}
</style>
