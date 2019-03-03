<template>
  <div id="app">
    <div class="pages">
      <router-view/>
    </div>
    <small>Made with love from Kampala, Uganda</small>
  </div>
</template>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
.pages {
  height: 100%;
  padding-left: 100px;
  padding-right: 100px;
  width: 100%;
}
</style>
