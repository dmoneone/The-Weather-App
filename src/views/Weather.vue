<template>
  <div class="weather">
    <select class="custom-select mr-sm-2" v-model="city">
      <option value="none">This city does not exist</option>
      <option value="Vinnytsia">Vinnytsia</option>
      <option value="Dnipropetrovsk">Dnipropetrovsk</option>
      <option value="Donetsk">Donetsk</option>
      <option value="Zhytomyr">Zhytomyr</option>
      <option value="Zaporizhzhia">Zaporizhzhia</option>
      <option value="Ivano-Frankivsk">Ivano-Frankivsk</option>
      <option value="Kyiv">Kyiv</option>
      <option value="Kirovohrad">Kirovohrad</option>
      <option value="Luhansk">Luhansk</option>
      <option value="Lutsk">Lutsk</option>
      <option value="Lviv">Lviv</option>
      <option value="Mykolaiv">Mykolaiv</option>
      <option value="Odessa">Odesa</option>
      <option value="Poltava">Poltava</option>
      <option value="Rivne">Rivne</option>
      <option value="Sevastopol">Sevastopol</option>
      <option value="Simferopol">Simferopol</option>
      <option value="Sumy">Sumy</option>
      <option value="Ternopil">Ternopil</option>
      <option value="Uzhhorod">Uzhhorod</option>
      <option value="Kharkiv">Kharkiv</option>
      <option value="Kherson">Kherson</option>
      <option value="Khmelnytskyi">Khmelnytskyi</option>
      <option value="Cherkasy">Cherkasy</option>
      <option value="Chernivtsi">Chernivtsi</option>
      <option value="Chernihiv">Chernihiv</option>
    </select>
    <button  class="btn btn-success" @click="loadForecast">load</button>
    <ul>
      <Loader v-if="loader" style="margin-top: 50px"/>
      <Forecast
        v-else
        v-bind:forecast="forecast"
        v-bind:showForecast="showForecast"
      />
    </ul>
  </div>
</template>

<script>
// @ is an alias to /src
import Forecast from '@/components/Forecast.vue'
import Loader from '@/components/Loader.vue'

export default {
  components: {
    Forecast,Loader
  },
  data() {
    return {
      city: '',
      forecast: {},
      showForecast: false,
      loader: false
    }
  },
  methods: {
    loadForecast() {
      this.loader = true;
      this.showForecast = true;
      //https://ipinfo.io/
      //http://api.openweathermap.org/data/2.5/weather?q=${this.city},ua&appid=50744a6264d8ebe36f256f3e998b39b2&units=metric
      fetch(`http://api.openweathermap.org/data/2.5/weather?q=${this.city},ua&appid=50744a6264d8ebe36f256f3e998b39b2&units=metric`)
        .then(res => res.json())
        .then(data => {
          setTimeout(()=>{
            this.forecast = data;
            this.loader = false
          },400)
        })
    }
  },
  mounted() {
      fetch('http://ip-api.com/json/?fields=61439')
        .then(res => res.json())
        .then(data => this.city = data.city)
        .then(()=>this.loadForecast())
  },
  watch: {
    forecast(v){
      console.log(v)
    }
  }
}
</script>

<style>
  .custom-select{
    max-width: 300px;
    width: 100%;
  }
</style>
