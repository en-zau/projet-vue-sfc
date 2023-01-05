<template>
  <div class="container mt-5">
    <div id="main">
      <div class="form">
        <h1 class="mb-3">
          <i class="fa-brands fa-apple"></i> Itunes Music Scrapper
        </h1>
        <div class="bar">
          <input
            type="search"
            class="form-control"
            aria-label="Default"
            aria-describedby="inputGroup-sizing-default"
            v-model="searchString"
            @change="MySearchQuery()"
            placeholder="Enter a artist name ..."
          />
        </div>
        <input
          type="button"
          class="btn btn-success m-3"
          value="Search"
          @click="MySearchQuery"
        />
      </div>
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
import axios from "axios";
const apiUrl =
  "https://itunes.apple.com/search?country=FR&media=podcast&entity=podcast&attribute=genreIndex&limit=30&term=";
export default {
  data() {
    return {
      searchString: "",
      array: null,
    };
  },
  methods: {
    fetchDataPromise: function (search = "") {
      console.log(apiUrl + search);
      axios
        .get(apiUrl + search)
        .then(async (response) => {
          console.log(response.data.results);
          this.array = await response.data.results;
        })
        .catch(function (error) {
          console.log(error);
        });
    },
    MySearchQuery: function () {
      let array = this.array;
      let searchString = this.searchString;
      if (!searchString) {
        return array;
      }
      searchString = searchString.trim().toLowerCase().replaceAll(" ", "+");
      console.log(searchString);
      this.fetchDataPromise(searchString);
      return array;
    },
  },
  computed: {},
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
