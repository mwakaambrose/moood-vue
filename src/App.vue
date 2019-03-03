<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/moods">Moods</router-link>
    </div> -->
    <!-- <sui-divider /> -->
    <div class="pages">
      <router-view/>
    </div>
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
