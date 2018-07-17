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
        <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" @click.native="handleModalOpen(item)"/>
    </div>
    <div class="loading" v-if="step===1 && loading"><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div></div>
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"/>
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
import Modal from "@/components/Modal.vue";

const API = "https://images-api.nasa.gov/";

export default {
  name: "Search",
  components: {
    Claim,
    SearchInput,
    HeroImage,
    Item,
    Modal
  },
  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: false,
      step: 0,
      searchValue: "",
      results: []
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    handleInput: debounce(function() {
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
    }, 500)
  }
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

.results {
  margin-top: 50px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;
  @media (min-width: 768px) {
    width: 90%;
    grid-template-columns: 1fr 1fr 1fr;
  }
}

.loading {
  margin-top: 100px;
  display: inline-block;
  position: relative;
  width: 64px;
  height: 64px;
}
.loading div {
  animation: loading 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  transform-origin: 32px 32px;
}
.loading div:after {
  content: " ";
  display: block;
  position: absolute;
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #000;
  margin: -3px 0 0 -3px;
}
.loading div:nth-child(1) {
  animation-delay: -0.036s;
}
.loading div:nth-child(1):after {
  top: 50px;
  left: 50px;
}
.loading div:nth-child(2) {
  animation-delay: -0.072s;
}
.loading div:nth-child(2):after {
  top: 54px;
  left: 45px;
}
.loading div:nth-child(3) {
  animation-delay: -0.108s;
}
.loading div:nth-child(3):after {
  top: 57px;
  left: 39px;
}
.loading div:nth-child(4) {
  animation-delay: -0.144s;
}
.loading div:nth-child(4):after {
  top: 58px;
  left: 32px;
}
.loading div:nth-child(5) {
  animation-delay: -0.18s;
}
.loading div:nth-child(5):after {
  top: 57px;
  left: 25px;
}
.loading div:nth-child(6) {
  animation-delay: -0.216s;
}
.loading div:nth-child(6):after {
  top: 54px;
  left: 19px;
}
.loading div:nth-child(7) {
  animation-delay: -0.252s;
}
.loading div:nth-child(7):after {
  top: 50px;
  left: 14px;
}
.loading div:nth-child(8) {
  animation-delay: -0.288s;
}
.loading div:nth-child(8):after {
  top: 45px;
  left: 10px;
}
@keyframes loading {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
