<template>
  <div class="container mt-5">
    <div id="main">
      <SearchBar
        searchUrl="https://itunes.apple.com/search?country=FR&media=podcast&entity=podcast&attribute=genreIndex&limit=30&term="
        title="Podcast"
        v-on:data_emit="array = $event"
      ></SearchBar>
      <div class="list-group" v-for="item in array" v-bind:key="item">
        <div
          class="list-group-item list-group-item-action mb-2"
          aria-current="true"
        >
          <div class="d-flex w-100">
            <img class="me-3" :src="item.artworkUrl100" />
            <div class="d-flex w-100 justify-content-between">
              <h5 class="mb-1">
                <a :href="item.trackViewUrl" target="_blank">{{
                  item.trackName
                }}</a>
              </h5>
            </div>
          </div>
          <p>
            Artist :
            <a :href="item.artistViewUrl" target="_blank">{{
              item.artistName
            }}</a>
          </p>
          <p>
            Style :
            <a :href="item.artistViewUrl" target="_blank">{{
              item.primaryGenreName
            }}</a>
          </p>
          <p>
            Date :
            <a :href="item.artistViewUrl" target="_blank">{{
              item.releaseDate
            }}</a>
          </p>
          <small></small>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import SearchBar from "@/components/SearchBar.vue";

export default {
  components: {
    SearchBar,
  },
  data() {
    return {
      array: [],
    };
  },
};
</script>

<style>
[v-cloak] {
  display: none;
}

* {
  margin: 0;
  padding: 0;
}

body {
  font-family: "Roboto", sans-serif;
  color: #5e5b64;
}

a:hover {
  text-decoration: none;
}

section,
footer,
header,
aside,
nav {
  display: block;
}
.form {
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: space-evenly;
}
.bar {
  width: 30rem;
}
</style>
