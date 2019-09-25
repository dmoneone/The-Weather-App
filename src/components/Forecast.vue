<template>
  <div class="wrap">
    <li v-if="showForecast">
      <div class="forecast" v-if="forecast.cod == 200">
        <span class="city">{{forecast.name}},{{forecast.sys.country}}</span>
        <span class="date">{{dateConverter}}</span>
        <span class="main">{{forecast.weather[0].main}}</span>
        <img v-bind:src="src" alt="">
        <span class="temp">{{forecast.main.temp}}°C</span>
        <span class="max-temp t">Max {{forecast.main.temp_max}}°C</span>
        <span class="min-temp t">Min {{forecast.main.temp_min}}°C</span>
        <span class="sky">{{forecast.weather[0].description}}</span>
        <span class="humidity">Humidity: {{forecast.main.humidity}}%</span>
        <span class="pressure">Pressure: {{forecast.main.pressure}}mm</span>
        <span class="sunset">Sunset: {{sunsetConverter}}</span>
        <span class="sunrise">Sunrise: {{sunriseConverter}}</span>
      </div>
      <div v-else style="font-weight: bold; font-size: 50px">404</div>
    </li>
    <span style="padding: 20px" v-else>Choose a city and push load.</span>
  </div>
</template>

<script>
export default {
  props:{
    forecast: Object,
    showForecast: Boolean
  },
  data() {
    return {
      src: "http://openweathermap.org/img/w/" + this.forecast.weather[0].icon + ".png",
      dt: this.forecast.dt,
      sunrise: this.forecast.sys.sunrise,
      sunset: this.forecast.sys.sunset
    }
  },
  computed: {
    dateConverter(){
             var t = new Date(this.dt*1000);
             var months = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
             var year = t.getFullYear();
             var month = months[t.getMonth()];
             var date = t.getDate();
             var dateTime = date+' '+month+' '+year;
             return dateTime;
    },
    sunriseConverter() {
        var t = new Date(this.sunrise*1000);
        var hour = t.getHours();
        var min = (t.getMinutes() < 10) ? "0"+t.getMinutes() : t.getMinutes();
        var sec = (t.getSeconds() < 10) ? "0"+t.getSeconds() : t.getSeconds();
        var dateTime = hour+':'+min+':'+sec ;
        return dateTime;
    },
    sunsetConverter() {
        var t = new Date(this.sunset*1000);
        var hour = t.getHours();
        var min = (t.getMinutes() < 10) ? "0"+t.getMinutes() : t.getMinutes();
        var sec = (t.getSeconds() < 10) ? "0"+t.getSeconds() : t.getSeconds();
        var dateTime = hour+':'+min+':'+sec ;
        return dateTime;
    }
  }

}
</script>

<style scoped>
  .wrap{
    display: -webkit-flex;
    display: -ms-flex;
    display: flex;
    justify-content: center;
  }
  li{
    list-style: none;
    box-sizing: border-box;
    max-width: 250px;
    width: 100%;
    margin-top: 30px;
  }
  span.city{
    padding-top: 10px;
    padding-bottom: 10px;
    font-weight: bold;
    font-size: 25px;

  }
  span{
    display: block;
    padding: 0;
  }
  .temp{
    font-size: 40px;
  }
  .main{
    font-weight: bold;
    font-size: 25px;
    padding-top: 10px;
  }
  .t{
    font-size: 12px;
    padding-top: 5px;
    &:first-child{
      padding-top: 20px;
    }
  }
  .sky{
    font-weight: bold;
    padding-top: 5px;
    padding-bottom: 5px;
  }
  .humidity, .pressure{
    padding-top: 5px;
    padding-bottom: 5px;
  }
  .sunrise, .sunset{
    padding-top: 5px;
    padding-bottom: 5px;
  }
  .forecast{
    border: 1px solid #2c3e50;;
    border-radius: 10px;
    padding: 30px;
    box-sizing: borde-box;
  }
  .date{
    font-weight: bold;
  }
</style>
