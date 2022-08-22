<template>
        <li class="position-relative h-350 overflow-hidden ps-3 mb-3">
            <img class="img-fluid" :src="`${baseMovies}${this.production.poster_path}` || `${errorPic}`" 
         :alt="production.title || production.name" />
       
        <span class="ms-3 p-3 active" >
            <li><span>Titolo: </span><strong class="text-uppercase">{{ production.title || production.name }}</strong></li>
            <li><span>Titolo Originale: </span> <strong class="text-uppercase">{{ production.original_title || production.original_name }}</strong></li>
            <li><span>Lingua: </span>
                <img class="language " v-if="hasFlag" :src="flagSrc" :alt="production.original_language">
                <p v-else><strong></strong>{{production.original_language}}</p>
            </li>
            <li><span>Descrizione: </span>   {{ production.overview }}</li>
            <li>
                <span>Voto: </span><i class="starColor fa-star" v-for="i in 5" :key="i" :class=" i <= setStar ? 'fa-solid fa-star' : 'fa-regular fa-star'"></i>
            </li>
        </span> 

        </li>     
   
</template>
<script>

export default{
    name: 'productionCard',
    data(){
        return{
             baseMovies:'https://image.tmdb.org/t/p/w342',
             errorPic :'https://www.informatique-mania.com/wp-content/uploads/2020/12/Netflix-error-U7353-5101.jpg',
             voteAverage : this.production.vote_average/2
        }
    },
    props:{
        production:Object
    },
    computed:{
        hasFlag(){
            const flags = ['it','en'];
            return flags.includes(this.production.original_language);
        },
        flagSrc(){
            
                return require(`../assets/flags/${this.production.original_language}.png`)
            
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

</style>