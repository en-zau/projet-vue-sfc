<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/music">Music</router-link> |
    <router-link to="/album">Album</router-link> |
    <router-link to="/artist">Artist</router-link> |
    <router-link to="/clip">Clip</router-link>
  </nav>
  <router-view />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
