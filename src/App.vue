<template>
  <router-view />
</template>

<style lang="scss">
@import url("@/assets/css/normalize");

@import url('https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300;0,400;0,500;0,600;0,700;1,300;1,400;1,500;1,600;1,700&display=swap');

// .bg-body {
//   --tw-bg-opacity: 1;
//   background-color: rgba(255,255,255,var(--tw-bg-opacity));
// }
// .dark .bg-body {
//   --tw-bg-opacity: 1;
//   background-color: rgba(45,51,62,var(--tw-bg-opacity));
// }

// .bg-accent {
//   --tw-bg-opacity: 1;
//   background-color: rgba(243,244,246,var(--tw-bg-opacity));
// }
// .dark .bg-accent {
//   --tw-bg-opacity: 1;
//   background-color: rgba(55,65,81,var(--tw-bg-opacity));
// }

// .bg-primary {
//     --tw-bg-opacity: 1;
//     background-color: rgba(67,184,131,var(--tw-bg-opacity));
// }

// .Cookie.Cookie--lv-theme {
//     background-color: #43b883!important;
//     color: #fafafa;
//     padding: 20px;
//     font-size: 1.1em;
//     width: 30em;
//     max-width: calc(100% - 40px);
//     display: block;
//     text-align: left;
//     left: 20px;
//     bottom: 20px;
//     border-radius: 6px;
// }
// .Cookie--lv-theme .Cookie__button {
//     background: #2d333e;
//     color: hsla(0,0%,100%,.75);
//     padding: 5px 20px;
//     border-radius: 6px;
//     transition: all .4s ease-out;
//     float: right;
//     margin: 0;
//     display: block;
// }

// p code {
//     font-size: .85em;
//     padding: 1px 8px;
//     margin: 0 5px;
//     background-color: rgba(67,184,131,.15);
//     color: #43b883;
// }

// .font-sans {
//     font-family: Rubik,sans-serif;
// }

// .text-gray-400 {
//     --tw-text-opacity: 1;
//     color: rgba(156,163,175,var(--tw-text-opacity));
// }

body {
  background: #1C1C2C;
}

::-webkit-scrollbar {
  width: 10px;
  height: 10px;
}
::-webkit-scrollbar-track {
  padding: 2px;
  border-radius: 100px;
}
::-webkit-scrollbar-thumb {
  border-radius: 100px;
  background-color: rgba(203, 219, 238, 0.5);
}

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
