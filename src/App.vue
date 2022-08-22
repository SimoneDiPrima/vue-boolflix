<template>
<div class="container">
  <SearchBar placeholder="scegli il tuo film preferito" @search="startSearch"/>
  <div class="d-flex flex-wrap" v-if ="word ===''">
    <h4 class="col-12 subtitlePage fw-bolder fst-italic text-center mb-4">&hearts; Everytime Everywhere only for you &hearts;</h4>
    
    <img class="col-3 wh-100" src="https://www.themoviedb.org/t/p/w600_and_h900_bestv2/kdYu7YJJP0uuGEuhUX5toqvBSog.jpg" alt="">
    <img class="col-3 wh-100" src="https://www.themoviedb.org/t/p/w600_and_h900_bestv2/vX6qhnZlPTJNrOoFNnUUkrqv1qo.jpg" alt="">
    <img class="col-3 wh-100" src="https://www.themoviedb.org/t/p/w600_and_h900_bestv2/q54qEgagGOYCq5D1903eBVMNkbo.jpg" alt="">
    <img class="col-3 wh-100" src="https://www.themoviedb.org/t/p/w600_and_h900_bestv2/6Xq0gAxrm8KMAKWP4KYYhPWoQXM.jpg" alt="">
    <h4 class="col-12 subtitlePage fw-bolder fst-italic text-center mt-4"><quote>"...May the force be with you"</quote></h4>
  </div>
   <ul class=" text-white mt-5 d-flex flex-wrap" >
      <productionCard id="Movies" title="Movies" class="col-lg-3 col-md-6 col-sm-12" v-for="movie in movies" :key="movie.id" :production="movie"/>
      <productionCard id="Series" title="Series" class="col-lg-3 col-md-6 col-sm-12" v-for="serie in series" :key="serie.id" :production="serie"/>
    </ul>
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
          title : true,
          word:''
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
        }
        
      this.fetchData(`/search/movie`,config,'movies');
      this.fetchData(`/search/tv`,config,'series');
      this.word = query;
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
.subtitlePage{
  color:$titlePage_color;
}
.wh-100{
  max-width:100%;
  max-height:100%;
}

</style>
