<template>
  <div class="header">
    <div class="d-flex wrap-header justify-content-center align-items-center">
      <a href="/"><img src="@/assets/img/logo_large.png" alt="Logo"></a>
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
    width: 100%;
    height: 100px;
    background-color: black;
    img{
      width: 400px;
      height: 70px;
      margin-right: 50px;
      padding: 0 50px;
      background-color: white;
    }
    input{
      width: 400px;
    }
  }

    
</style>