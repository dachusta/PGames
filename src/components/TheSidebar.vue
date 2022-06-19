<template>
  <div class="sidebar">
    <div class="logo">
      PGames
    </div>
    <nav class="nav">
      <!-- <div class="link">Home</div> -->
      <!-- <router-link class="link" to="/">Home</router-link> -->
      <router-link
        class="link"
        to="/games"
      >
        Games
      </router-link>
      <router-link
        class="link"
        to="/game-details"
      >
        Game details
      </router-link>
      <div class="link">
        Top
      </div>
      <div class="link">
        4
      </div>
      <div class="link">
        5
      </div>
    </nav>
  </div>
</template>

<script setup>
</script>

<style lang="scss" scoped>
.sidebar {
  background: #27293f;
  padding: 10px;
  z-index: 1;

  .logo {
    position: sticky;
    top: 10px;
  }

  .nav {
    display: flex;
    flex-direction: column;
    position: sticky;
    padding: 30px;
    top: 28px;

    .link {
      font-weight: bold;
      color: inherit;

      &.router-link-exact-active {
        color: #42b983;
      }
    }
  }
}
</style>
