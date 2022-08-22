<template>
<div class="container">
  <SearchBar placeholder="scegli il tuo film preferito" @search="startSearch"/>
  <div>
    <h1 v-if="title">che cosa vuoi vedere stasera?</h1>
    <ul class=" text-white mt-5 d-flex flex-wrap" v-else>
      <productionCard class="col-lg-3 col-md-6 col-sm-12" v-for="movie in movies" :key="movie.id" :production="movie"/>
      <productionCard class="col-lg-3 col-md-6 col-sm-12" v-for="serie in series" :key="serie.id" :production="serie"/>
    </ul>
  </div>
</div>

</template>

<script>
import axios from 'axios';

import SearchBar from "./components/SearchBar.vue";
import productionCard from './components/productionCard.vue';
export default{
  name:'App',
  components:{
    SearchBar,
    productionCard
  },
  data(){
      return{
        movies:[ ],
        series:[ ],
        api:{
            language:'it-IT',
            baseUri:'https://api.themoviedb.org/3',
            key:'bf0f896563566d6ee072f696caf75297'
          }, 
          title : true
        }
    },
    
   methods:{
    startSearch(query){
      if(!query){
        this.movies=[];
        this.series=[];
        return;
      }
        const { language , key } = this.api;
        const config = {
            params:{
                api_key : key,
                language,
                query,
            },
        };
      this.fetchData(`/search/movie`,config,'movies');
      this.fetchData(`/search/tv`,config,'series');
    },
    fetchData(endpoint,config,target){
      axios.get(`${this.api.baseUri}${endpoint}`, config).then((res)=>{
      this[target] = res.data.results;
    })
    }
   
   }
}

</script>

<style lang="scss">
@import './assets/scss/style.scss';

</style>
