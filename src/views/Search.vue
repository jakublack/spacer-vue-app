<template>
  <div class="wrapper">
    <Claim />
    <SearchInput />
    
    
  </div>
</template>

<script>
// eslint-disable-next-line

import axios from "axios";
import debounce from "lodash.debounce";
import Claim from "@/components/Claim.vue";
import SearchInput from "@/components/SearchInput.vue";

const API = "https://images-api.nasa.gov/";

export default {
  name: "Search",
  components: {
    Claim,
    SearchInput,
  },
  data() {
    return {
      searchValue: "",
      results: []
    };
  },
  methods: {
    handleInput: debounce(function() {
      axios
        .get(`${API}/search?q=${this.searchValue}&media_type=image`)
        .then(response => {
          this.results = response.data.collection.items;
        })
        .catch(error => {
          console.log(error);
        });
    }, 500)
  }
};
</script>


<style lang="scss" scoped>

    .wrapper {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin: 0;
        padding: 30px;
        width: 100%;
        height: 100vh;
        background-image: url('../assets/heroimage.jpg');
        background-repeat: no-repeat;
        background-size: cover;
        background-position: 80% 0%;


    }

</style>

