<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input @keyup.enter="fetchWeather" v-model="query" type="text" class="search-bar" placeholder="Search...">
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'" >
        <div class="location-box">
          <div class="location"> {{weather.name}}, {{weather.sys.country}} </div>
          <div class="date">{{moment().format('MMMM Do YYYY')}}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{Math.round(weather.main.temp)}}°C</div>
          <div class="weather">{{weather.weather[0].main}}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
  export default {
    name: 'App',
    data () {
      return {
        api_key: '3d865259c8c6c755a8f105c1fb22db4b',
        url_base: 'https://api.openweathermap.org/data/2.5/',
        query:'',
        weather: {}
      }
    },

    methods: {
      setResults (results) {
        this.weather = results;
      },
      fetchWeather() {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResults);
      },
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: 'montserrat', sans-serif;
}

#app{
  background-image: url('assets/Hot.jpg');
  background-size: cover;
  background-position: bottom;
  transition: .5s;
}

main{
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, .25), rgba(0, 0, 0, .75));
}
input::placeholder{
  color: white;
  transition: .5s;
}

input:focus::placeholder{
  color: rgba(0, 0, 0, .6);
}
.search-box{
  width: 100%;
  margin-bottom: 30px;
}

.search-bar{
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  outline: none;
  appearance: none;
  border: none;
  background: none;
  box-shadow: 0 0 12px rgba(0, 0, 0, .3);
  background-color: rgba(255, 255, 255, .5);
  border-radius: 16px 16px 4px 4px;
  transition: 0.5s;
}

.search-box .search-bar:focus{
  box-shadow: 0 0 25px rgba(0, 0, 0, .3);
  background-color: rgba(255, 255, 255, .8);
  border-radius: 16px;
}

.location-box .location {
  color: white;
  font-size: 32px;
  font-weight: 600;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, .25);
  text-transform: uppercase;
}

.location-box .date {
  color: rgba(255, 255, 255, .8);
  font-size: 20px;
  font-weight: 300;
  text-align: center;
  font-style: italic;
}

.weather-box {
  text-align: center;
}

.weather-box .temp{
  display: inline-block;
  padding: 10px 25px;
  color: white;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, .3);
  background-color: rgba(255, 255, 255, .3);
  border-radius: 20px;
  margin: 30px 0;
  box-shadow: 3px 6px rgba(0, 0, 0, .3);
}

.weather-box .weather{
  color:  white;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, .3);
}
</style>
