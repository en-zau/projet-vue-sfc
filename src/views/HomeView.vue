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
              <small
                ><span
                  class="badge bg-dark"
                  style="font-weight: lighter"
                  v-if="item.collectionExplicitness === 'explicit'"
                  >Explicit</span
                ></small
              >
            </div>
          </div>
          <p>
            Artist :
            <a :href="item.artistViewUrl" target="_blank">{{
              item.artistName
            }}</a>
          </p>
          <a
            class="btn btn-outline-danger"
            :href="item.trackViewUrl"
            target="_blank"
            ><i class="fa-solid fa-cart-shopping"></i> for
            {{ item.trackPrice }}€</a
          >
          <small></small>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
const apiUrl =
  "https://itunes.apple.com/search?country=FR&media=music&entity=musicTrack&attribute=songTerm&limit=30&term=";
export default {
  data() {
    return {
      searchString: "",
      array: null,
    };
  },
  methods: {
    fetchDataPromise: function (search = "") {
      const self = this;
      // console.log(apiUrl + search)
      this.axios
        .get(apiUrl + search)
        .then(function (response) {
          console.log(response.data.results);
          self.array = response.data.results;
          // console.log(self.commits[0].html_url);
        })
        .catch(function (error) {
          console.log(error);
        });
    },
    MySearchQuery: function () {
      let array = this.array,
        searchString = this.searchString;

      if (!searchString) {
        return array;
      }

      searchString = searchString.trim().toLowerCase().replaceAll(" ", "+");
      console.log(searchString);
      this.fetchDataPromise(searchString);

      // array = array.filter(function (item) {
      //     if (
      //         item.title
      //             .toLowerCase()
      //             .startsWith(searchString) === true
      //     ) {
      //         return item;
      //     }
      // });
      return array;
    },
  },
  computed: {},
};
</script>
