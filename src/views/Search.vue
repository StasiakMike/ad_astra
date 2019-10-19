<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
  <transition name="slide">
    <img src="../assets/ad astra.png" class="logo" v-if="step === 1">
  </transition>
  <transition name="fade">
    <HeroImage v-if="step === 0"/>
  </transition>
  <Claim v-if="step === 0"/>
  <Searchinput v-model="searchValue" @input="handleInput" :dark="step === 1" />
  <div class="results" v-if="results && !loading && step === 1">
    <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" @click.native="handleModalOpen(item)"/>
  </div>


        <!--
        <ul>
          <li v-for="item in results" :key="item.data[0].nasa_id">
            <p>{{ item.data[0].description}}</p>
          </li>
        </ul>
        -->
    <div class="loader" v-if="step === 1 && loading"><div></div><div></div><div></div></div>
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"/>

  </div>

</template>


<script>

import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import Searchinput from '@/components/Searchinput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const myApi = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  components: {
    Claim,
    Searchinput,
    HeroImage,
    Item,
    Modal,
  },
  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
    };
  },

  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    // eslint-disable-next-line
    handleInput: debounce(function () {
      this.loading = true;
      console.log(this.searchValue);
      axios.get(`${myApi}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss" scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 30px;
  min-height: 100vh;
  position: relative;

  &.flexStart {
    justify-content: flex-start;
  }
}


.fade-enter-active, .fade-leave-active {
  transition: opacity .5s ease;
}
.fade-enter, .fade-leave-to  {
  opacity: 0;
}

.slide-enter-active, .slide-leave-active {
  transition: margin-top .5s ease;
}
.slide-enter, .slide-leave-to  {
  margin-top: -50px;
}

.logo {
  height: 40px;
  width: 70px;
  position: absolute;
  top: 30px;
}

.results {
  margin-top: 50px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;

  @media (min-width: 768px) {
   grid-template-columns: 1fr 1fr 1fr;

  }
}

.loader {
  margin-top: 100px;
  display: inline-block;
  position: relative;
  width: 64px;
  height: 64px;

  @media (min-width: 768px) {
  width: 90px;
  height: 90px;
  }
}
.loader div {
  display: inline-block;
  position: absolute;
  left: 6px;
  width: 13px;
  background: #1e3d4a;
  animation: loader 1.2s cubic-bezier(0, 0.5, 0.5, 1) infinite;
}
.loader div:nth-child(1) {
  left: 6px;
  animation-delay: -0.24s;
}
.loader div:nth-child(2) {
  left: 26px;
  animation-delay: -0.12s;
}
.loader div:nth-child(3) {
  left: 45px;
  animation-delay: 0;
}
@keyframes loader {
  0% {
    top: 6px;
    height: 51px;
  }
  50%, 100% {
    top: 19px;
    height: 26px;
  }
}


</style>
