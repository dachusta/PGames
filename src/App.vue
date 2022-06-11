<template>
  <router-view/>
</template>

<style lang="scss">
@import url("@/assets/css/normalize");

@import url('https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300;0,400;0,500;0,600;0,700;1,300;1,400;1,500;1,600;1,700&display=swap');

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-family: 'Open Sans', sans-serif;
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
