<template>
  <div>
    <p class="forecast-title" v-if="Object.keys(computedForecasts).length != 0">3 Hour Forecast for next 4 days</p>
    <div class="forecast-card-wrap">
      <div class="forecast-card" v-for="(day, key) in computedForecasts" :key="key">
        <div class="basic-card">
          <div>
            <span class="forecast-card-title"> {{ getDay(day[0].dt) }} </span>
          </div>
          <div class="forecast-card-body">
            <p v-for="forecast in day" :key="forecast.dt">
              {{  moment.unix(forecast.dt).format("hh:mma") }}:
              {{ forecast.weather[0].description }}
              <img
                :src="getImgUrl(forecast.weather[0].icon)"
                class="forecast-icon"
                alt="forecast icon"
              />, Temp ({{ forecast.main.temp }}°), Pressure ({{
                forecast.main.pressure
              }}), Humidity ({{ forecast.main.humidity }})
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
    
  <script>
import moment from "moment";
export default {
  name: "ForecastWeather",
  props: {
    computedForecasts: Object
  },
  data: () => ({
    moment,
  }),
  methods: {
    getDay(unixTimeStamp) {
      return moment.unix(unixTimeStamp).format("dddd");
    },
    getImgUrl(data) {
      return `https://openweathermap.org/img/wn/${data}@2x.png`;
    },
  },
};
</script>
    
    <style scoped>
.forecast-title {
  display: block;
  font-size: 25px;
  text-align: center;
  font-weight: 500;
  margin: 50px 0 20px;
}
.forecast-card-wrap {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  flex-wrap: wrap;
}
.forecast-card {
  background-color: transparent;
  border-radius: 10px;
  box-shadow: none;
  margin-top: 20px;
  padding: 20px;
  border: 1px solid #f2f0e9;
  border-radius: 20px;
  box-shadow: rgb(196 225 192 / 20%) 0px 8px 24px;
  margin-bottom: 20px;
  max-width: 500px !important;
}
.basic-card {
  padding: 20px 20px 10px 20px;
  margin-bottom: 20px;
}
.forecast-card-title {
  display: block;
  font-size: 18px;
  text-align: left;
  line-height: 100%;
  font-weight: 600;
  margin: 10px 0px;
}
.forecast-card-body {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.forecast-icon {
  vertical-align: middle;
  width: 30px;
  height: 20px;
}
</style>
    