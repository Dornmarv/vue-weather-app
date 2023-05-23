<template>
  <div class="card" v-if="typeof weather.main != 'undefined'">
    <div class="basic-card">
      <div class="card-header">
        <span class="card-title">
          {{ weather.name }}, {{ weather.sys.country }}
        </span>
        <div class="card-title">
          {{ moment().format("dddd Do MMM YYYY") }}
        </div>
      </div>
      <div class="card-body">
        <div class="card-inner">
          <div>
            <div class="current-temp">{{ Math.round(weather.main.temp) }}°</div>
            <div>
              <img
                :src="getImgUrl(weather.weather[0].icon)"
                class="weather-img"
                alt="weather img"
              />
              <span class="weather-description">
                {{ weather.weather[0].description }}
              </span>
            </div>
          </div>
        </div>
        <div class="card-inner">
          <div class="basic-others">
            <div class="box">
              <img
                src="@/assets/images/temp-high.svg"
                class="weather-icon"
                alt="weather icon"
              />
              <div class="box-info">
                <p class="text name">Today's High</p>
                <p class="text value">
                  {{ Math.round(weather.main.temp_max) }}°c
                </p>
              </div>
            </div>
            <div class="box">
              <img
                src="@/assets/images/temp-low.svg"
                class="weather-icon"
                alt="weather icon"
              />
              <div class="box-info">
                <p class="text name">Today's Low</p>
                <p class="text value">
                  {{ Math.round(weather.main.temp_min) }}°c
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="more-card" v-show="showMore">
        <div class="card-body">
          <div class="card-inner">
            <div>
              <div class="box">
                <img
                  src="@/assets/images/wind.svg"
                  class="weather-icon"
                  alt="weather img"
                />
                <div class="box-info">
                  <p class="text name">Wind Speed</p>
                  <p class="text value">
                    {{ weather.wind.speed }}
                  </p>
                </div>
              </div>
              <div class="box">
                <img
                  src="@/assets/images/humidity.svg"
                  class="weather-icon"
                  alt="weather icon"
                />
                <div class="box-info">
                  <p class="text name">Humidity</p>
                  <p class="text value">
                    {{ weather.main.humidity }}
                  </p>
                </div>
              </div>
              <div class="box">
                <img
                  src="@/assets/images/pressure.svg"
                  class="weather-icon"
                  alt="weather icon"
                />
                <div class="box-info">
                  <p class="text name">Pressure</p>
                  <p class="text value">
                    {{ weather.main.pressure }}
                  </p>
                </div>
              </div>
            </div>
          </div>
          <div class="card-inner">
            <div>
              <div class="box">
                <img
                  src="@/assets/images/sunrise.svg"
                  class="weather-icon"
                  alt="weather icon"
                />
                <div class="box-info">
                  <p class="text name">Sunrise</p>
                  <p class="text value">
                    {{ moment.unix(weather.sys.sunrise).format("hh:mm a") }}
                  </p>
                </div>
              </div>
              <div class="box">
                <img
                  src="@/assets/images/sunset.svg"
                  class="weather-icon"
                  alt="weather icon"
                />
                <div class="box-info">
                  <p class="text name">Sunset</p>
                  <p class="text value">
                    {{ moment.unix(weather.sys.sunset).format("hh:mm a") }}
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="btn-container">
        <button @click="toggleText()" class="toggle-btn" v-if="!showMore">
          Show More
        </button>
        <button @click="toggleText()" class="toggle-btn" v-else>
          Show Less
        </button>
      </div>
    </div>
  </div>
</template>
  
<script>
import moment from "moment";
export default {
  name: "CurrentWeather",
  data: () => ({
    moment,
    showMore: false,
  }),
  methods: {
    getImgUrl(icon) {
      return `https://openweathermap.org/img/wn/${icon}@2x.png`;
    },
    toggleText() {
      this.showMore = !this.showMore;
    }
  },
  props: {
    weather: Object,
  },
};
</script>
  
  <style scoped>
.card {
  width: 100%;
  background-color: transparent;
  border-radius: 10px;
  box-shadow: none;
  margin-top: 20px;
  border: 1px solid #f2f0e9;
  border-radius: 20px;
  box-shadow: rgb(196 225 192 / 20%) 0px 8px 24px;
}
.basic-card {
  padding: 20px 20px 10px 20px;
  margin-bottom: 20px;
}
.card-header {
  margin-bottom: 30px;
}
.card-title {
  display: block;
  font-size: 16px;
  text-align: center;
  line-height: 100%;
  font-weight: 500;
  margin-bottom: 10px;
}
.card-body {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.card-inner {
  display: flex;
  flex-direction: column;
}
.current-temp {
  line-height: 1;
  display: block;
  font-size: 90px;
  font-weight: bold;
  text-shadow: -7px 7px 0 #5f5252;
}
.weather-img {
  vertical-align: middle;
  width: 70px;
  margin-left: -17px;
}
@media screen and (max-width: 540px) {
  .weather-img {
    width: 40px;
    margin-left: -8px;
  }
  .btn-container {
    margin-top: 20px;
  }
}
.btn-container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.weather-description {
  text-transform: capitalize;
}
.box {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  margin-bottom: 20px;
}
.box-info {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
}
.weather-icon {
  vertical-align: middle;
  width: 30px;
  margin-right: 10px;
}
.text {
  margin-bottom: 0px;
  margin-top: 0px;
}
.name {
  font-weight: 400;
  font-size: 14px;
}
.value {
  font-weight: 600;
  font-size: 18px;
}
.toggle-btn {
  border: 1px solid #f2f0e9 !important;
  background-color: #0a0b0e !important;
  color: #f2f0e9;
  text-transform: capitalize;
  height: 30px;
  font-size: 15px;
  font-weight: 600;
  border-radius: 5px;
  cursor: pointer;
  padding: 5px 10px;
}
</style>
  