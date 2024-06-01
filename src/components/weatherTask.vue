<template>
  <div class="container">
    <div class="weather__header">
      <form @submit.prevent="fetchWeather" class="weather__search">
        <input v-model="query" type="text" placeholder="Enter city name" class="weather__searchform"/>
      </form>
    </div>
    <div class="weather__body" v-if="weather">
        <h1 class="weather__city">{{ weather.name }}</h1>
        <div class="weather__datetime">
        </div>
        <div class="weather__forecast">{{ weather.main.temp }}°C</div>
        <div class="weather__forecast">Wind: {{ weather.wind.speed }}</div>
        <div class="weather__icon">
        </div>
        <p class="weather__temperature">
          {{ weather.weather[0].description }}
        </p>
        <p class="weather__minmax">
          Humidity: {{ weather.main.humidity }}
        </p>
        <div class="weather__minmax">
            <p>Min: 12</p>
            <p>Max: 16</p>
        </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import axios from 'axios';

export default {
  setup() {
    const query = ref('');
    const weather = ref(null);

    const fetchWeather = async () => {
      if (!query.value) return;

      const API_KEY = '36883c7ef4a934ffb972ffecd89b719a';
      const url = `https://api.openweathermap.org/data/2.5/weather?q=${query.value}&units=metric&appid=${API_KEY}`;

      try {
        const response = await axios.get(url);
        weather.value = response.data;
      } catch (error) {
        console.error('Error fetching weather data:', error);
      }
    };

    return {
      query,
      weather,
      fetchWeather,
    };
  },
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Poppins', sans-serif;
}

.container {
    background: #171717;
    color: #fff;
    padding: 2rem;
    max-width: 1500px;
    margin: 4rem auto;
    border-radius: 10px;
}

.weather__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

input {
    border: none;
    background: #1e1e1e;
    outline: none;
    color: #fff;
    padding: 0.5rem 2.5rem;
    border-radius: 5px;
}

input::placeholder {
    color: #fff;
}

.weather__search {
    position: relative;
}

.weather__search i {
    position: absolute;
    left: 10px;
    top: 10px;
    font-size: 15px;
    color: #fff;
}

.weather__units {
    font-size: 1.5rem;
}

.weather__units span {
    cursor: pointer;
}

.weather__units span:first-child {
    margin-right: 0.5rem;
}

.weather__body {
    text-align: center;
    margin-top: 3rem;
}

.weather__datetime {
    margin-bottom: 2rem;
    font-size: 14px;
}

.weather__forecast {
    background: #1e1e1e;
    display: inline-block;
    padding: 0.5rem 1rem;
    border-radius: 30px;
}

.weather__icon img {
    width: 100px;
}

.weather__temperature {
    font-size: 1.75rem;
}

.weather__minmax {
    display: flex;
    justify-content: center;
}

.weather__minmax p {
    font-size: 14px;
    margin: 0.5rem;
}

.weather__info {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 1rem;
    margin-top: 3rem;
}

.weather__card {
    display: flex;
    align-items: center;
    background: #1e1e1e;
    padding: 1rem;
    border-radius: 10px;
}

.weather__card i {
    font-size: 1.5rem;
    margin-right: 1rem;
}

.weather__card p {
    font-size: 14px;
}


@media(max-width: 936px){
    .container {
        width: 90%;
    }

    .weather__header {
        flex-direction: column;
    }

    .weather__units {
        margin-top: 1rem;
    }
}


@media(max-width: 400px){
    .weather__info {
        grid-template-columns: none;
    }
}
</style>
