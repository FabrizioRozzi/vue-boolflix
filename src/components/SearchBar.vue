<template>
  
  <div class="d-flex wrap-header justify-content-center align-items-center">
      <form>
        <input 
          v-model="text"
          type="text"
          placeholder="Inserisci un titolo di un film"
        >
        <button 
          @click.prevent="search"
          class="btn-primary ms-3">Cerca
        </button>

      </form>
    
  </div>
</template>

<script>
export default {
  name : 'SearchBar',
  data(){
    return{
      text : ''
    }
  },
  methods:{
    search(){
      //console.log(this.text);
      this.$emit("searching", this.text)
      this.text=""
    }
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
    button{
     
    }
  }
</style>