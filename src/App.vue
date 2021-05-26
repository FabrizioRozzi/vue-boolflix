<template>
  <div id="app">
    <SearchBar />
    <Card 
      v-for="film in this.arrFilm"
      :key="film.id"
      :film="film"
    />
  </div>
</template>

<script>
  import axios from 'axios'
  import SearchBar from "@/components/SearchBar.vue"
  import Card from "@/components/Card.vue"

export default {
  name: 'App',
  components: {
    SearchBar,
    Card
  },
  data(){
    return{
      arrFilm : [],
      apiURL : "https://api.themoviedb.org/3/search/movie",
      apiKey : '186ab9d59ce76af2382545bfd0366db4',
      query : 'fantozzi'
    }
  },
  created(){
    axios.get(this.apiURL,{
      params:{
        api_key : this.apiKey,
        query : this.query,
        language: 'it-IT'
      }
    })
    .then(resp =>{
      this.arrFilm = resp.data.results
      console.log(this.arrFilm);
    })
    .catch(err =>{
      console.log(err);
    })
  }
}
</script>

<style lang="scss">
  @import '@/assets/style/general'
</style>
