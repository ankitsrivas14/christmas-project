<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&display=swap');
body{
  margin: 0;
  padding: 0;
  background-color: #eeeef0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 100vw;
  height: 100vh;
  background-image: url('./assets/main-bg.png');
  background-size: cover;
  @media screen and (max-width: 800px) {
    height: 100%;
  }
}
</style>
