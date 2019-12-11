<template>
  <v-app>
    <v-container>
      <div>
        <Navbar />
      </div>
      <div class="mt-4">
        <v-card max-width="400">
          <v-list-item two-line>
            <v-list-item-content>
              <v-list-item-title class="headline">{{ weather.name }}</v-list-item-title>
              <v-list-item-subtitle>{{ weather.weather[0].main }}</v-list-item-subtitle>
              <v-list-item-subtitle>Humidity: {{ weather.main.humidity }}%</v-list-item-subtitle>
              <v-list-item-subtitle>Pressure: {{ weather.main.pressure }} hpa</v-list-item-subtitle>
              <v-list-item-subtitle>Wind: {{ weather.wind.speed }}m/s ({{ weather.wind.deg }})&deg;</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>

          <v-card-text>
            <v-row align="center">
              <v-col class="display-3" cols="6">{{ temp }}&deg;C</v-col>

              <v-col cols="6">
                <v-img :src="icon" alt="weather icon=" width="92"></v-img>
              </v-col>
              <v-list-item-subtitle>Maximum Temperature: {{ temp_max }}&deg;C</v-list-item-subtitle>
              <v-list-item-subtitle>Maximum Temperature: {{ temp_min }}&deg;C</v-list-item-subtitle>
            </v-row>
          </v-card-text>
        </v-card>
      </div>

      <div class="mx-auto mt-4">
        <v-col cols="6" md="4">
          <v-form @submit.prevent="getWeatherInfo">
            <v-text-field label="Type Your City" filled dense v-model="city"></v-text-field>
          </v-form>
        </v-col>
      </div>
    </v-container>
  </v-app>
</template>

<script>
import Navbar from '../components/Navbar'
export default {
  data() {
    return {
      city: 'Dhaka'
    }
  },
  asyncData({ params, $axios }) {
    return $axios
      .$get(
        `https://api.openweathermap.org/data/2.5/weather?q=Dhaka
        &appid=${process.env.weatherAppId}`
      )
      .then(res => {
        return {
          weather: res
        }
      })
  },
  methods: {
    getWeatherInfo() {
      this.$axios
        .$get(
          `https://api.openweathermap.org/data/2.5/weather?q=
        ${this.city}&appid=${process.env.weatherAppId}`
        )
        .then(res => (this.weather = res))
    }
  },

  computed: {
    icon() {
      return this.weather.weather
        ? `https://openweathermap.org/img/wn/${this.weather.weather[0].icon}.png`
        : ''
    },
    temp() {
      return this.weather.main ? Math.round(this.weather.main.temp - 273) : ''
    },
    temp_max() {
      return this.weather.main
        ? Math.round(this.weather.main.temp_max - 273)
        : ''
    },
    temp_min() {
      return this.weather.main
        ? Math.round(this.weather.main.temp_min - 273)
        : ''
    }
  },

  components: {
    Navbar
  }
}
</script>

<style scoped>
a {
  text-decoration: none;
  color: white;
}
</style>