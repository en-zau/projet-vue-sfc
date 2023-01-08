<template>
  <div class="form">
    <h1 class="mb-3"><i class="fa-brands fa-apple"></i> Search</h1>
    <div class="bar">
      <input
        type="search"
        class="form-control"
        aria-label="Default"
        aria-describedby="inputGroup-sizing-default"
        v-model="searchString"
        @change="MySearchQuery()"
        placeholder="Enter a music name ..."
      />
    </div>
    <input
      type="button"
      class="btn btn-success m-3"
      value="Search"
      @click="MySearchQuery"
    />
  </div>
</template>
<script>
import axios from "axios";

// const apiUrl =
//   "https://itunes.apple.com/search?country=FR&media=music&entity=musicTrack&attribute=songTerm&limit=30&term=";
export default {
  props: ["searchUrl"],
  data() {
    return {
      searchString: "",
      array: null,
    };
  },
  methods: {
    fetchDataPromise: function (search = "") {
      // console.log(apiUrl + search)
      axios
        .get(this.searchUrl + search)
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
      this.emitSearch();
      return array;
    },
    emitSearch() {
      this.$emit("data_emit", this.array);
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
