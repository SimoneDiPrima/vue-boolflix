<template>
    <section :id="id">
        <h2 class="text-center text-success title" :title="title">{{title}}</h2>
        <li class="position-relative h-350 overflow-hidden ps-3 mb-3">
            <img v-if="production.poster_path" class="img-fluid" :src="`${coverPoster}`" 
         :alt="production.title || production.name" />
            <img v-else :src="placeholderSrc" class="wh-100 p-3" alt="Coming Soon">
            <figcaption class="h5 text-warning mt-2 text-center fst-italic">Coming Soon</figcaption>
       
            <span class="ms-3 p-3 active" >
                <li><span>Titolo: </span><strong class="text-uppercase">{{ production.title || production.name }}</strong></li>
                <li><span>Titolo Originale: </span> <strong class="text-uppercase">{{ production.original_title || production.original_name }}</strong></li>
                <li><span>Lingua: </span>
                    <img class="language " v-if="hasFlag" :src="flagSrc" :alt="production.original_language">
                    <p v-else><strong>{{production.original_language}}</strong></p>
                </li>
                <li><span>Descrizione: </span>{{ production.overview }}</li>
                <li>
                    <span>Voto: </span><i class="starColor fa-star" v-for="i in 5" :key="i" :class=" i <= setStar ? 'fa-solid fa-star' : 'fa-regular fa-star'"></i>
                </li>
            </span> 

        </li>  
  </section>
</template>
<script>

export default{
    name: 'productionCard',
    data(){
        return{
             baseMovies:'https://image.tmdb.org/t/p/w342',
             placeholderPic :"../assets/logo.png",

             voteAverage : this.production.vote_average/2
        }
    },
    props:{
        production:Object , 
        id:String,
        title :String
    },
    computed:{
        coverPoster(){
            const cover = this.baseMovies + this.production.poster_path
            return cover;
        },
        hasFlag(){
            const flags = ['it','en'];
            return flags.includes(this.production.original_language);
        },
        flagSrc(){
            
                return require(`../assets/flags/${this.production.original_language}.png`)
            
        },
        placeholderSrc(){
              return require(`../assets/placePic.png.png`)
        },
       
        setStar(){
            let stars = Math.ceil(this.voteAverage);
            return stars;
        }
    }
}
</script>
<style scoped>
img.language{
    width:60px;
    height:30px;
}
.starColor{
    color:goldenrod;
}
.active{
    cursor:pointer;
    position:absolute;
    top:0;
    left:0;
   right:0;
   bottom:0;
    z-index:10;
   background-color: rgba(0, 0, 0, 0.8);
    overflow-y:auto;
    font-size: 10px;
   visibility:hidden;
   
}
.wh-100{
    max-width:100%;
    max-height:100%;
}

.h-350{
    height:350px;
}
img{
    display: inline-block;
}

li:hover span
{
    visibility: visible;
}
.title{
    cursor:pointer;
}
</style>