<template>
  <div id="app">
    <SearchBar 
      @searching="startSearch"
    />
    <div class="max">
      <h1 v-if="this.result.movie.length > 0">
        Film trovati:
      </h1>
      <Film 
        type='movie'
        v-for="film in result.movie"
        :key="film.id"        
        :film="film"
      />

        
    

    
      <h1 v-if="this.result.tv.length > 0">
        Serie tv trovate:
      </h1>
      <Serie 
        type='tv'
        v-for="serie in result.tv"
        :key="serie.id"
        :serie="serie"
      />
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import SearchBar from "@/components/SearchBar.vue"
  import Film from "@/components/Film.vue"
  import Serie from "@/components/Serie.vue"
 

export default {
  name: 'App',
  components: {
    SearchBar,
    Film,
    Serie
  },
  data(){
    return{
      titles:{
        'movie' : 'Film trovati',
        'tv' : 'Serie tv trovate' 
      },
      result:{
        'movie': [],
        'tv':[]
      },
      apiURL : "https://api.themoviedb.org/3/search/",
      apiKey : '186ab9d59ce76af2382545bfd0366db4',
      query : ''
      
    }
  },
    methods:{
      startSearch(obj){
        this.reset();
        if(obj.type === 'all'){
          this.searched(obj.text, 'movie');
          this.searched(obj.text, 'tv');
        }else{
          this.searched(obj.text, obj.type);
          
        }
      },

      reset(){
        this.result.movie = [];
        this.result.tv = [];
      },

      searched(text , type){
        
        axios.get(this.apiURL+type,{
        params:{
          api_key : this.apiKey,
          query : text,
          language: 'it-IT'
        }
        })
    
        .then(resp =>{
          this.result[type] = resp.data.results;
          console.log(this.result);
        })
        .catch(err =>{
          console.log(err);
        })
        
      },

      
  
    }
}
</script>

<style lang="scss">
  @import '@/assets/style/general';
  h1{
    color:white;
  }
  .max{
    max-width: 1200px;
    margin: 0 auto;
  }
</style>
