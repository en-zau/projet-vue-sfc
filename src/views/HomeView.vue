<template>
  <div class="container mt-5">
    <div id="main">
      <div class="title">
        <h1>Welcome on our Itunes Scapper</h1>
        <h3>Please refer to our categories to search what you desire.</h3>
      </div>
      <div class="menu mt-5">
        <div class="list-group list">
          <router-link
            to="/music"
            class="list-group-item list-group-item-action"
            >Music</router-link
          >
          <router-link
            to="/artist"
            class="list-group-item list-group-item-action"
            >Artist</router-link
          >
          <router-link
            to="/podcast"
            class="list-group-item list-group-item-action"
            >Podcast</router-link
          >
        </div>
      </div>
    </div>
  </div>
</template>
<script></script>
<style>
.menu {
  display: flex;
  justify-content: center;
  text-align: center;
}
.list {
  width: 20rem;
}
.title {
  text-align: center;
}
</style>
