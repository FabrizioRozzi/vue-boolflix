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
        <h6>{{serie.original_language}}</h6>
      </li>
      <li>
        <h6>{{serie.vote_average}}</h6>
      </li>
    </ul>
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

</style>