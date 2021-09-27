<template>
  <div class="app" v-bind:class="{'isLoaded': isLoaded === true}">
    <HeroImage />
    <div style="z-index: 1; padding-top: 80px;">
      <SiteTitle />
      <SearchInput v-model="searchValue"  @input="handleInput" :value="searchValue"/>    
    </div>
    <LoadingSpinner v-if="isLoading === true" class="loadingSpinner"/>
    <WeatherBox 
      v-if="isLoaded === true" 
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
import LoadingSpinner from '@/components/LoadingSpinner.vue';

const API = 'https://api.openweathermap.org/data/2.5/weather';
const apiID = 'a7643e5b5c8f5093e7112ed4af01e38e';

export default {
  name: 'App',
  components: {
    HeroImage,
    SiteTitle,
    SearchInput,
    WeatherBox,
    LoadingSpinner,
  },
  data() {
    return {
      searchValue: '',
      results: { },
      isLoaded: false,
      isLoading: false,
    }
  },
  methods: {
    
    handleInput:debounce(function(event) {
      
      this.searchValue = event.target.value;
      axios.get((`${API}?q=${this.searchValue}&APPID=${apiID}&units=metric`))
        .then((response) => {
          this.isLoading = true;
          this.isLoaded = false;
          setTimeout(()=> {
            this.results = response.data;
            this.isLoaded = true;
            this.isLoading = false;
          }, 1000)
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
    padding-top: 80px;

    &.isLoaded {

      @media(min-width: 768px){
        justify-content: space-evenly;
      }
    }
  }
  
  .loadingSpinner {
    margin-top: 50px;
  }
</style>
