<template>
  <div
    class="mainContainer"
    :class="
      typeof weatherObject.main !== 'undefined' && weatherObject.main.temp > 20
        ? 'mainContainer1'
        : ''
    "
  >
    <main>
      <div class="searchSection">
        <input
          type="text"
          class="search-bar"
          placeholder="Search..."
          v-model="searchQuery"
          @keypress.enter="getWeather"
        />
      </div>
      <div
        class="weatherSection"
        v-if="typeof weatherObject.main !== 'undefined'"
      >
        <h1 class="headingCity">{{ weatherObject.name }}</h1>
        <div class="tempClass">
          <h1>{{ Math.round(weatherObject.main.temp) }}°C</h1>
        </div>
        <div class="maxminSection">
          <div class="myWed">
            <p>Max</p>
            <h4>{{ Math.round(weatherObject.main.temp_max) }}°C</h4>
          </div>
          <div class="myWed">
            <p>Min</p>
            <h4>{{ Math.round(weatherObject.main.temp_min) }}°C</h4>
          </div>
        </div>
        <div class="myHumi">
          <p>Humidity {{ weatherObject.main.humidity }}</p>
          <p>feels like {{ Math.round(weatherObject.main.feels_like) }}</p>
          <p>Wind Speed {{ weatherObject.wind.speed }}</p>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  //https://api.openweathermap.org/data/2.5/weather?q=barisal&units=metric&APPID=f81fb3fc039e7bbe1a0ce38ee9365800
  data() {
    return {
      base_api_url: "https://api.openweathermap.org/data/2.5/",
      api_key: "f81fb3fc039e7bbe1a0ce38ee9365800",
      searchQuery: "",
      weatherObject: {},
    };
  },
  methods: {
    async getWeather() {
      const url = `${this.base_api_url}weather?q=${this.searchQuery}&units=metric&APPID=${this.api_key}`;
      const { data } = await axios.get(url);
      this.weatherObject = data;
      console.log(this.weatherObject);
    },
  },
};
</script>

<style>
body {
  font-family: "montserrat", sans-serif;
  margin: 0px;
  padding: 0px;
}
.mainContainer {
  widows: 100%;
  height: 100vh;

  background-image: url("./assets/cold.jpg");

  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
.mainContainer1 {
  widows: 100%;
  height: 100vh;

  background-image: url("./assets/warm.jpg");

  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
main {
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  );
  height: 100vh;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.searchSection {
  display: flex;
  width: 50%;
  align-items: center;
  justify-content: center;
}
.search-bar {
  width: 60%;
  height: 40px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  background-color: rgba(240, 248, 255, 0.487);
  padding: 10px;
  border-radius: 10px;
  color: rgb(87, 87, 87);
  margin-top: 20px;
  font-size: 22px;
}
.weatherSection {
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.headingCity {
  font-size: 70px;
  color: rgba(255, 255, 255, 0.727);
  margin: 0px;
  margin-top: 20px;
}
.tempClass {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 52px;
  margin: 0px;
  color: rgba(255, 255, 255, 0.802);
}
.tempClass > h1 {
  margin: 0px;
}
.maxminSection {
  display: flex;
}
.myWed {
  display: flex;
  align-items: center;
}
.myWed > p {
  margin: 0px;
  font-size: 19px;
  margin-right: 5px;
  font-weight: bold;
  color: #c8d6e5;
}
.myWed > h4 {
  margin: 0px;
  margin-right: 20px;
  font-size: 29px;
  font-weight: bold;
  color: #c8d6e5;
}
.myHumi {
  display: flex;
}
.myHumi > p {
  margin: 30px;
  font-size: 29px;
  font-weight: 600;
  color: #c8d6e564;
}
</style>
