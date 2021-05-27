<template>
  <div>
    
    <ul>
      <li>
        <h4>{{film.title}}</h4>
      </li>
      <li>
        <h5>{{film.original_title}}</h5>
      </li>
      <li>
        <flag :iso="film.original_language === 'en' ? 'gb' : film.original_language" />
      </li>
      <li>
        <div class="star"
          v-for="index in 5"  :key="index"
        >
          <i
            v-if="index > Math.round(film.vote_average/2)"
            class="far fa-star">
          </i>

          <i 
            v-else
            class="fas fa-star">
          </i>
        </div>
      </li>
    </ul>

    <img :src=" 'http://image.tmdb.org/t/p/w342' + film.poster_path " alt="">
    
  </div>
</template>

<script>
export default {
  name : 'Film',
  props:{
    film : Object,
    
    type : String

  },
 

}
</script>

<style >
  .star{
    display: inline-block;
  }
</style>