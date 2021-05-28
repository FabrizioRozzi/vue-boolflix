<template>
<div class="card-container">
  <div class="flip-card">
    <div class="flip-card-inner">
      <div class="flip-card-front">
        <img 
          v-if="film.poster_path != null"
          :src=" 'http://image.tmdb.org/t/p/w342' + film.poster_path " alt="" style="width:180px;height:300px;">
        <img 
          v-else
          src="@/assets/img/default.jpg" alt="">  
      </div>
      <div class="flip-card-back">
        <ul>
          <li>
            Titolo: {{film.name}}
          </li>
          <li
            v-if="film.title != film.original_title"
          >
            
              Titolo originale: {{film.original_title}}
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
          <li class="p">
            <p >{{film.overview}}</p>
          </li>
        </ul>
      </div>
    </div>
</div>
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

<style lang="scss" scoped>
*{
  font-size: 12px;
  line-height: 15px;
}
.star{
  display: inline-block;
}

.card-container{
  display: inline-flex;
  justify-content: space-between;
  
  padding: 5px 10px;
}
  
.flip-card {
  width:180px;
  height:300px;
  background-color: transparent;
  perspective: 1000px; /* Remove this if you don't want the 3D effect */
}

/* This container is needed to position the front and back side */
.flip-card-inner {
  
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

/* Do an horizontal flip when you move the mouse over the flip box container */
.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

/* Position the front and back side */
.flip-card-front, .flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
}

/* Style the front side (fallback if image is missing) */
.flip-card-front {
  
  color: black;
}

/* Style the back side */
.flip-card-back {
  padding-left: -25px;
  background-color: black;
  color: white;
  transform: rotateY(180deg);
  overflow: auto;
}

.p{
  
}

ul{
  width: 100%;
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