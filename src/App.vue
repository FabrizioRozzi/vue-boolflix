<template>
  <div id="app">
    <SearchBar 
      @searching="startSearch"
    />
    <div class="popular"
      v-if="this.result.movie.length < 1 && this.result.tv.length < 1"
    >
      <h3>I film piú popolari: </h3>
      <div class="cont">
        <Film
          type='movie'
          v-for="film in result.popolariMv"
          :key="film.id"        
          :film="film"
        />
      </div>
      
      <h3>Le serie piú popolari: </h3>
      <div class="cont">
        <Serie 
          type='tv'
          v-for="serie in result.popolariTv"
          :key="serie.id"        
          :serie="serie"
        />
      </div>

      
    </div>
    <div class="max">
      <h3 v-if="this.result.movie.length > 0">
        Film trovati:
      </h3>
      <div class="cont">
        <Film 
          type='movie'
          v-for="film in result.movie"
          :key="film.id"        
          :film="film"
        />
      </div>

        
    

    
      <h3 v-if="this.result.tv.length > 0">
        Serie tv trovate:
      </h3>
      <div class="cont">
        <Serie 
          type='tv'
          v-for="serie in result.tv"
          :key="serie.id"
          :serie="serie"
        />
      </div>
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
        'tv' : 'Serie tv trovate',
     
      },
      result:{
        'movie': [],
        'tv':[],
        'popolariMv' : [],
        'popolariTv' : []
      },
      apiURL : "https://api.themoviedb.org/3/search/",
      apiKey : '186ab9d59ce76af2382545bfd0366db4',
      query : '',
      
    }
  },
    created(){
     let type = 'popolariMv'
      axios.get('https://api.themoviedb.org/3/movie/popular',{
          params:{
            api_key: this.apiKey,
            language: 'it-IT'
          }
        })
        .then(res => {
           this.result[type] = res.data.results;
           console.log(this.result[type]);
        })
        .catch(err => {
          console.log(err);
        })
    
      let typetv = 'popolariTv'
      axios.get('https://api.themoviedb.org/3/tv/popular',{
          params:{
            api_key: this.apiKey,
            language: 'it-IT'
          }
        })
        .then(res => {
           this.result[typetv] = res.data.results;
           console.log(this.result[typetv]);
        })
        .catch(err => {
          console.log(err);
        })
    
  
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
  h3{
    color:white;
  }
  .max, .popular{
    max-width: 1200px;
    height: 500px;
    margin: 0 auto;
  }

  .cont{
    display: flex;
    overflow-x: auto;
  }

  * {
    scrollbar-width: thin;
    scrollbar-color:red #252525;
  }
  /* Chrome, Edge, and Safari */
  *::-webkit-scrollbar {
    width: 10px;
  }
  *::-webkit-scrollbar-track {
    background: #252525;
  }
  *::-webkit-scrollbar-thumb {
    background-color: #9F0000;
    border-radius: 5px;
    border: 1px solid black;
  }
</style>
