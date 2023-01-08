<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/music">Music</router-link> |
    <router-link to="/artist">Artist</router-link> |
    <router-link to="/podcast">Podcast</router-link>
  </nav>
  <router-view />
</template>

<style>
nav {
  padding-top: 30px;
  text-align: center;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
