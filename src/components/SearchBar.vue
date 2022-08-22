<template>
<header class="d-flex justify-content-between mt-4">
  <h1 class="fw-bold">Boolflix</h1>
  <div>
    <input type="text" class="me-2 rounded-pill"  placeholder = "cerca il tuo film preferito" v-model="term" @keyup="emitSearch">
    <button class="text-white mainButton rounded-pill fw-semibold" @click="emitSearch" type="button">Cerca</button>
  </div>
</header>
</template>

<script>
export default{
    name:'SearchBar',
    data(){
      return {
        term:""
      }
    },
    methods:{
      emitSearch(){
        this.$emit('search',this.term)
      }
    }

}
</script>
<style scoped lang="scss">
@import '../assets/scss/style.scss';
.mainButton{
  background-color : $titlePage_color;

}
</style>