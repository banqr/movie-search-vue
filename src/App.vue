<template>
  <div id="app">
    <h3>Movie search</h3>
    <form @submit.prevent="hello">
      <div class="row">
        <div class="six columns">
          <label for="movie">Your movie</label>
          <input v-model="movie" class="u-full-width" type="text" id="movie">
        </div>
      </div>
      <input class="button-primary" type="submit" value="Submit">
    </form>
    <img v-bind:src="imgage" v-if="seen">
  </div>
</template>

<script>
const giphy_url_1 = 'https://api.giphy.com/v1/gifs/search?api_key=tRoV6ISux00Pr8859b5RJF0p0BSACosj&q='
const giphy_url_2 = '&limit=25&offset=0&rating=G&lang=en'
const axios = require('axios')
export default {
  name: 'app',
  data() {
    return {
      seen: false,
      movie: '',
      gifs: [],
      imgage: ''
    }
  },
  methods: {
    hello: function(){
      axios.get(`${giphy_url_1}${this.movie}${giphy_url_2}`)
        .then(res => this.gifs = res.data)
        .then(dejta => {
          this.seen = true
          this.imgage = dejta.data[0].images.downsized.url
          this.movie = ''    
          console.log(dejta.data[0].images.downsized.url)
          })  
    }
  },
}
</script>

<style>
</style>
