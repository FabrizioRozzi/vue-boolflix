<template>
<div class="card-container" v-if="film.poster_path != null">
  <div class="flip-card">
    <div class="flip-card-inner">
      <div class="flip-card-front">
        <img 
          :src=" 'http://image.tmdb.org/t/p/w342' + film.poster_path " alt="" style="width:180px;height:300px;"> 
        
      </div>
      <div class="flip-card-back">
        <ul>
          <li>
            <strong>Titolo : </strong> {{film.title}}
          </li>
          <li
            v-if="film.title != film.original_title"
          >
            
              <strong>Titolo originale: </strong> {{film.original_title}}
          </li>
          <li>
           <strong>Lingua: </strong> <flag :iso="film.original_language === 'en' ? 'gb' : film.original_language" />
          </li>
          <li>
            <strong>Voto: </strong>
            <div class="star"
              :style="`width:${7*film.vote_average}px`"
            >
              <div class="cont-star">
                <i class="fas fa-star"></i>
                <i class="fas fa-star"></i>
                <i class="fas fa-star"></i>
                <i class="fas fa-star"></i>
                <i class="fas fa-star"></i>
              </div>
              
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
  overflow-x: hidden;
  .cont-star{
    width: 70px;
  }
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