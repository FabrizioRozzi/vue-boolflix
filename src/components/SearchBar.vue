<template>
  
  <div class="d-flex wrap-header justify-content-center align-items-center">
      <form>
        <input 
          v-model="text"
          type="text"
          placeholder="Inserisci un titolo di un film"
        >
        <button 
          @click.prevent="$emit('searching', {text:text, type:'movie'})"
          class="btn-primary ms-3">Film
        </button>
        <button 
          @click.prevent="$emit('searching', {text:text, type:'tv'})"
          class="btn-primary ms-3">Serie
        </button>
        <button 
          @click.prevent="$emit('searching', {text:text, type:'all'})"
          class="btn-primary ms-3">All
        </button>

      </form>
    
  </div>
</template>

<script>
export default {
  name : 'SearchBar',
  data(){
    return{
     
        text : '',
        type : ''
 
      
    }
  },
  methods:{
    
  }

}
</script>

<style lang="scss" scoped>
  .wrap-header{
    height: 100px;
    width: 100%;
    input{
      width: 400px;
    }
  }
</style>