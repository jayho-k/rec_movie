<template>
  <div v-if="movie.poster_path">
    <a href="">
      <div class="screen" @click="routingDetail(movieId)" >
        <div class="top">{{movie.title}}</div>
        <div class="bottom">{{ movie.release_date }}</div>
        <img :src="posterPath" alt="">
      </div> 
    </a>
  </div>

</template>

<script>
import router from '@/router'
const imgUrl='https://image.tmdb.org/t/p/w500/'
export default {
  name: 'MovieCard',
  props:{
    movie:Object,
  },
  computed:{
    posterPath(){

      return imgUrl+this.movie.poster_path
    }
  },
  methods:{
    routingDetail(){
      router.push({
        name:'detail',
        params:{movie_id:this.movie.movie_id?this.movie.movie_id:this.movie.id}
        })
    },
  }

}
</script>

<style  lang="scss" scoped>
img {
    max-width: 100%;
    height: 285px;
    cursor: pointer;
    border-radius: 10px;
}

// .top{ font-size:30px;}
.screen {position:relative;overflow:hidden;}
.screen .top {position:absolute;bottom:150%;left:30px;z-index:2;color:#fff;font-size:22px;font-weight:900;transition:all .35s;}
.screen .bottom {position:absolute;top:150%;left:30px;z-index:2;color:#fff;font-size:15px;transition:all .35s;}
// .screen img {width:100%;}
.screen::after {content:'';display:block;position:absolute;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,.5);z-index:1;opacity:0;transition:all .35s;}
a:hover .top {bottom:52%;}
a:hover .bottom {top:52%;}
a:hover .screen::after {opacity:1;}

</style>