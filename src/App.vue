<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Slider</router-link> |
      <router-link to="/Forms">Forms</router-link> |
      <router-link to="/Blocks">Blocks</router-link>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
body {
  margin: 0;
  background-color: #e5e5e5;
}

#app {
  font-family: Roboto, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000;
  // width: 1440px;
  // margin: 0 auto;
}

#nav {
  padding: 10px;

  a {
    font-weight: bold;
    color: #000;

    &.router-link-exact-active {
      color: #000;
    }
  }
}
</style>
