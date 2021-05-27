<template>
  <div>
    <ul>
      <li>
        <h4>{{serie.name}}</h4>
      </li>
      <li>
        <h5>{{serie.original_name}}</h5>
      </li>
      <li>
        <flag :iso="serie.original_language === 'en' ? 'gb' : serie.original_language" />
      </li>
      <li>
        <div class="star"
          v-for="index in 5"  :key="index"
        >
          <i
            v-if="index > Math.round(serie.vote_average/2)"
            class="far fa-star">
          </i>

          <i 
            v-else
            class="fas fa-star">
          </i>
        </div>
      </li>
    </ul>
    <img :src=" 'http://image.tmdb.org/t/p/w342' + serie.poster_path " alt="">
  </div>
    
    
</template>

<script>
export default {
  name : 'Serie',
  props:{
    serie : Object
  },
}
</script>

<style>
  .star{
    display: inline-block;
  }
</style>