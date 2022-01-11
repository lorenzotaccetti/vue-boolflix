<template>
  <div id="app">
    <Header @searchClicked="searchClicked" />
    <Main :details="researchArray" />
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
      researchArray: [],
    }
  },
  methods: {
    searchClicked: function(element){
      this.researchText = element
      
      axios.get('https://api.themoviedb.org/3/search/movie', {
        params: {
          api_key: 'eb32925ee4340f32b75ef0f48a3de4d6',
          query: this.researchText
        }
      })
      .then((response) => {
        this.researchArray = [ ...response.data.results];
      });
    },

  },
};
</script>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

</style>
