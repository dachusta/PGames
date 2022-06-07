<template>
  <router-view/>
</template>

<style lang="scss">
@import url("@/assets/css/normalize");

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
}

.wrapper {
  display: grid;
  grid-template-columns: 250px 1fr;
  background: #1C1C2C;
  color: #CBDBEE;
  position: relative;
  min-height: inherit;
}
</style>
