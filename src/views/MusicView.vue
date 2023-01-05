<template>
  <div class="container mt-5">
    <div id="main">
      <SearchBar
        searchUrl="https://itunes.apple.com/search?country=FR&media=music&entity=musicTrack&attribute=songTerm&limit=30&term="
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
