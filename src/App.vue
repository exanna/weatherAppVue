<template>
  <div class="app" v-bind:class="{'loaded': loaded === true}">
    <HeroImage />
    <SiteTitle />
    <SearchInput v-model="searchValue"  @input="handleInput" :value="searchValue"/>    
    <WeatherBox 
      v-if="loaded === true" 
      :temperature="results.main.temp"
      :main="results.weather.main"
      :pressure="results.main.pressure"
      :humidity="results.main.humidity"
      :windSpeed="results.wind.speed"
      :cloudy="results.clouds.all" 
    />    
  </div>
</template>

<script>

import axios from 'axios';
import debounce from 'lodash.debounce';
import HeroImage from '@/components/HeroImage.vue';
import SiteTitle from '@/components/SiteTitle.vue';
import SearchInput from '@/components/SearchInput.vue';
import WeatherBox from '@/components/WeatherBox.vue'

const API = 'https://api.openweathermap.org/data/2.5/weather';
const apiID = 'a7643e5b5c8f5093e7112ed4af01e38e';

export default {
  name: 'App',
  components: {
    HeroImage,
    SiteTitle,
    SearchInput,
    WeatherBox,
  },
  data() {
    return {
      searchValue: '',
      results: { },
      loaded: false,
    }
  },
  methods: {
    
    handleInput:debounce(function(event) {
      
      this.searchValue = event.target.value;
      axios.get((`${API}?q=${this.searchValue}&APPID=${apiID}&units=metric`))
        .then((response) => {
          this.results = response.data;
          this.loaded = true;
        }) 
        .catch((error) => console.log(error));
    }, 500),
  },
};
</script>

<style lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');

  * {
    box-sizing: border-box;
  }

  body,
  html {
    margin: 0;
    padding: 0;
  }

  .app {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    font-family: 'Montserrat', sans-serif;
    width: 100%;
    height: 100vh;
    overflow: hidden;

    &.loaded {
      justify-content: space-evenly;
    }
  }
  

</style>
