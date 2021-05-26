<template>
  <div id="app">
    <SearchBar 
      @searching="searched"
    />
    <Card 
      v-for="film in arrFilm"
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
      query : ''
    }
  },
    methods:{
      searched(text){
        
        axios.get(this.apiURL,{
        params:{
          api_key : this.apiKey,
          query : text,
          language: 'it-IT'
        }
      })
    
      .then(resp =>{
         this.arrFilm = resp.data.results
        
      })
      .catch(err =>{
        console.log(err);
      })
        }
        
    }
  
  
}
</script>

<style lang="scss">
  @import '@/assets/style/general'
</style>
