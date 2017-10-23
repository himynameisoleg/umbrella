<template>
  <div class="hello">
    <button @click="getWeather()">Umbrella?</button>
    <h2>{{ umbrella }}</h2>
    <h4>{{ description }}.</h4>
  </div>
</template>

<script>
export default {
  data () {
    return {
      umbrella: '',
      description: '',
      key: 'apikey=gn5l8vw37h1p5ao6sozdSJ7GlNYBdF30&',
      city: 'q=chicago&',
      language: 'language=en-us',
      locatonURL: 'http://dataservice.accuweather.com/locations/v1/cities/autocomplete?',
      weatherURL: 'http://dataservice.accuweather.com/forecasts/v1/daily/1day/348308?apikey=gn5l8vw37h1p5ao6sozdSJ7GlNYBdF30&language=en-us&details=false&metric=false',
      locationKey: '348308' // for Chicago
    }
  },
  methods: {
    // getLocation () {
    //   // fetches array of location based on autocomplete input
    //   fetch(this.locatonURL + this.key + this.city + this.language)
    //     .then((resp) => resp.json())
    //     .then(function (data) {
    //       console.log(data)
    //       // Your code for handling the data you get from the API
    //     })
    //     .catch(function (error) {
    //       console.log(error)
    //     })
    // },
    getWeather () {
      let self = this
      fetch(this.weatherURL)
        .then((resp) => resp.json())
        .then(function (data) {
          let condition = data.Headline.Category
          self.description = data.Headline.Text
          if (condition === 'rain') self.umbrella = 'Better Grab an Umbrella!'
          else self.umbrella = 'Not Today'
        })
        .catch(function (error) {
          console.log(error)
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
