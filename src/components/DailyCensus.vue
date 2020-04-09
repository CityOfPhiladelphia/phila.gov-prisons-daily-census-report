<template>
  <div>
    {{ censusData }}
  </div>
</template>

<script>
import axios from "axios";
// import Vue from "vue";

const endpoint = "https://api.phila.gov/inmate-locator/census?gatekeeperKey=c1cfa6750fa0517fbdefeb90a1464004";

export default {
  name: "DailyCensus",
  data: function() {
    return {
      censusData: [],
      loading: false,
      failure: false,
      empty: false,
   
    };
  },

  mounted() {
    this.fetchData();
  },

  watch: {
  },

  methods: {
    fetchData: function() {
      this.loading = true;
      axios
        .get(endpoint)
        .then(response => {
          this.censusData = response.data
          this.failure = false;
          this.loading = false;
        })
        .catch(e => {
          console.log(e);
          this.loading = false;
          this.failure = true;
        });
    },
  }
};
</script>

<style scoped>
.clear-search-btn {
  position: absolute;
  top: 16px;
  right: 70px;
  padding: 0;
  font-size: 20px;
  background-color: #fff;
  opacity: 0.8;
  z-index: 999;
  cursor: pointer;
  color: rgba(60, 60, 60, 0.5);
}
</style>
