<template>
<header class="d-flex justify-content-between mt-4">
  <h1>Boolflix</h1>
  <div>
    <input type="text" class="me-3"  placeholder = "cerca il tuo film preferito" v-model="term" @keyup="emitSearch">
    <button class="btn btn-danger" @click="emitSearch" type="button">Cerca</button>
  </div>
</header>
</template>

<script>
export default{
    name:'SearchBar',
    data(){
      return {
        term:" "
      }
    },
    methods:{
      emitSearch(){
        this.$emit('search',this.term)
      }
    }

}
</script>