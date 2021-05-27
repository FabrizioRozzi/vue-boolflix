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
        <h6>{{film.original_language}}</h6>
      </li>
      <li>
        <h6>{{film.vote_average}}</h6>
      </li>
    </ul>

    
    
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

</style>