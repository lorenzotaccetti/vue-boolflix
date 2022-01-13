<template>
  <div id="app">
    <!-- Header -->
    <Header @searchClicked="searchClicked" />
    <!-- Main -->
    <Main 
    :movies="moviesArray" 
    :tvseries="tvSeriesArray" 
    :text="researchText" 
    :starWarsFilm="starWarsArray" />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Main from './components/Main.vue';
import axios from 'axios';

export default {
  name: "App",
  components: {
    Header,
    Main
  },
  data: function(){
    return {
      researchText: '',
      moviesArray: [],
      tvSeriesArray: [],
      starWarsArray: [],
      api_key: 'eb32925ee4340f32b75ef0f48a3de4d6',
    }
  },
  methods: {
    searchClicked: function(element){
      // Collego il dato dell'input al data in App
      this.researchText = element;
      
      // Chiamata all'API per i film
      axios.get('https://api.themoviedb.org/3/search/movie', {
        params: {
          api_key: this.api_key,
          query: this.researchText
        }
      })
      .then((response) => {
        // Riempio l'array nei data con le informazioni date dall'API
        this.moviesArray = response.data.results;
      });

      // Chiamata all'API per le serie tv
      axios.get('https://api.themoviedb.org/3/search/tv',{
        params: {
          api_key: this.api_key,
          query: this.researchText
        }
      }).then((response) => {
        // Riempio l'array nei data con le informazioni date dall'API
        this.tvSeriesArray = response.data.results
      });
    },

  },
  created: function(){
    // Chiamata all'API per film star wars
    axios.get('https://api.themoviedb.org/3/search/movie', {
      params:{
        api_key: this.api_key,
        query: 'star-wars',
      }
    }).then((response) => {
      this.starWarsArray = response.data.results
    });
  }
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Raleway:ital,wght@0,400;1,400;1,700&family=Roboto+Condensed:wght@300;400&family=Vujahday+Script&display=swap');

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background-color: black;
  font-family: 'Raleway', sans-serif;
}

img{
  width: 100%;
  height: 100%;
}

</style>
