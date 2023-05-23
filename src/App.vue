<template>
  <div class="container">
    <Header msg="Weather App" />
    <div class="wrap">
      <div class="weather-wrap">
        <SearchBar />
      </div>
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import SearchBar from "./components/SearchBar.vue";

export default {
  name: 'App',
  components: {
    Header,
    SearchBar
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
