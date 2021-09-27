<template>
   <div class="weatherBoxWrapper">
      <p class="temperature"><span>{{ Math.floor(temperature) }} &#176;C</span></p>
      <p class="otherParameters">Pressure: <span>{{ pressure }} hPa</span></p>
      <p class="otherParameters">Humidity: <span>{{ humidity }} %</span></p>
      <p class="otherParameters">Speed of wind: <span>{{ windSpeed }} m/s</span></p>
      <p class="otherParameters">Cloudy: <span>{{ cloudy }} %</span></p>
    </div>    
</template>

<script>
export default {
   name: 'WeatherBox',
   props: {
      temperature: {
         type: Number, 
         required: true,
      },      
      pressure: {
         type: Number,
         required: true,
      },
      humidity: {
         type: Number,
         required: true,
      },
      windSpeed: {
         type: Number,
         required: true,
      },
      cloudy: {
         type: Number,
         required: true,
      },  
   },
   data() {
      return {

      }
   },
};
</script>

<style  scoped lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Ultra&display=swap');
   .weatherBoxWrapper {
      z-index: 1;
      color: white;
      font-size: 20px;
      text-align: center;
      min-width: 300px;
      background-color: rgba(0,0,0, .25);
      border-radius: 40px;
      padding: 30px;
      
      span {
         font-family: 'Ultra', serif;
      }
   }

   .temperature, 
   .otherParameters {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 18px;
   }

   .temperature {
      flex-direction: column;
      span {
         font-size: 50px;
      }
   }
</style>