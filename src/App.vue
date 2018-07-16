<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
      <transition name="slide">
          <img src="./assets/logo.svg" class="logo" alt="" v-if="step===1">
      </transition>
    <transition name="fade">
        <HeroImage v-if="step === 0" />
    </transition>
    <Claim  v-if="step===0" />
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="results" v-if="results && !loading && step === 1">
        <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id"/>
    </div>
  </div>
</template>

<script>
// eslint-disable-next-line

import axios from "axios";
import debounce from "lodash.debounce";
import Claim from "@/components/Claim.vue";
import SearchInput from "@/components/SearchInput.vue";
import HeroImage from "@/components/HeroImage.vue";
import Item from "@/components/Item.vue";


const API = "https://images-api.nasa.gov/";

export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
    HeroImage,
    Item
  },
  data() {
    return {
      loading: false,
      step: 0,
      searchValue: "",
      results: []
    };
  },
  methods: {
    handleInput: debounce(function () {
      console.log(this.searchValue);
      this.loading = true;

      axios
        .get(`${API}/search?q=${this.searchValue}&media_type=image`)
        .then(response => {
          this.loading = false;
          this.step = 1;

          this.results = response.data.collection.items;
        })
        .catch(error => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800");

* {
  box-sizing: border-box;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  font-family: Montserrat, sans-serif;
  font-size: 12px;
  margin: 0;
  padding: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.slide-enter-active,
.slide-leave-active {
  transition: margin-top 0.3s ease;

}

.slide-enter,
.slide-leave-to {
    margin-top: -50px;
}
.wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
  margin: 0;
  padding: 30px;
  width: 100%;
  min-height: 100vh;
  &.flexStart {
    justify-content: flex-start;
  }
}
.logo {
    position: absolute;
    top: 40px;

}
</style>
