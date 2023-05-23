<template>
  <div class="container">
    <Header msg="Weather App" />
    <div class="wrap">
      <div class="weather-wrap">
        <SearchBar />
        <CurrentWeather :weather="weather" />
      </div>
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import SearchBar from "./components/SearchBar.vue";
import CurrentWeather from './components/CurrentWeather.vue';
import moment from "moment";
import axios from "axios";

export default {
  name: 'App',
  components: {
    Header,
    SearchBar,
    CurrentWeather
  },
  data: () => ({
    api_key: "6a4d10009b90c42565cefef88b5bf366",
    url_base: "https://api.openweathermap.org/data/2.5/",
    weather: {},
    currentLocation: {},
    latitude: "",
    longitude: "",
    moment,
  }),
  methods: {
    async fetchWeather() {
      try {
        const res = await axios.get(
          `${this.url_base}weather?lat=${this.latitude}&lon=${this.longitude}&units=metric&APPID=${this.api_key}`
        );
        this.weather = res.data;
        const forecastRes = await axios.get(
          `${this.url_base}forecast?lat=${this.latitude}&lon=${this.longitude}&units=metric&APPID=${this.api_key}`
        );

        this.forecasts = forecastRes.data.list;
        let finalRes = forecastRes.data.list;
        Object.keys(this.sortedForecasts).forEach((key) => {
          delete this.sortedForecasts[key];
        });
        for (let i = 0; i < finalRes.length; i++) {
          let day = this.getDay(finalRes[i].dt);
          if (!this.sortedForecasts[day]) {
            this.sortedForecasts[day] = [];
          }
          this.sortedForecasts[day].push(finalRes[i]);
        }
      } catch (error) {
        console.log(error);
      }
    },
    async getCurrentLocation() {
      try {
        const res = await axios.get(
          "https://ipgeolocation.abstractapi.com/v1/?api_key=a4be84b7b5e74cddbf89da513717659d"
        );
        document.getElementById("location").value = res.data.city;
        this.currentLocation = res.data;
        this.latitude = res.data.latitude;
        this.longitude = res.data.longitude;
      } catch (error) {
        console.log(error);
      }
    },
    getDay(unixTimeStamp) {
      return moment.unix(unixTimeStamp).format("dddd");
    },
  },
  async mounted() {
    await this.getCurrentLocation();
    const google = window.google;
    const autocomplete = new google.maps.places.Autocomplete(
      document.getElementById("location")
    );

    autocomplete.addListener("place_changed", () => {
      const place = autocomplete.getPlace();
      this.latitude = place.geometry.location.lat();
      this.longitude = place.geometry.location.lng();
    });
  },
  watch: {
    longitude() {
      this.fetchWeather();
    },
  },
}
</script>

<style>
@font-face {
  font-family: avenir;
  font-weight: bold;
  src: url("./assets/fonts/AvenirNext-DemiBold.ttf");
}
@font-face {
  font-family: avenir;
  font-weight: normal;
  src: url("./assets/fonts/AvenirNext-Regular.ttf");
}
@font-face {
  font-family: avenir;
  font-weight: 500;
  src: url("./assets/fonts/AvenirNext-Medium.ttf");
}
#app {
  width: 100%;
  height: 100%;
  color: #f2f0e9;
  min-height: 100vh;
  height: 100%;
}
html {
  background-color: #0a0b0e;
  font-family: avenir;
}
.container {
  margin: 0 auto;
  max-width: 1280px;
  width: 90%;
  display: flex;
  justify-content: center;
  flex-direction: column;
}
.wrap {
  display: flex;
  flex-direction: row;
  justify-content: center;
}
.weather-wrap {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 40vw !important;
}
@media screen and (max-width: 540px) {
  .weather-wrap {
    width: 80vw !important;
  }
}
</style>
