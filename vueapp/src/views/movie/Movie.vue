<template>
<div>
  <ul>
      <li class="movie" v-for="movie in movieList" :key="movie.id">
          <div class="movie-img">
              <img :src="movie.images.large" alt="">

          </div>
          <div class="movie-info">
              <div class="movie-info-title">{{movie.title}}
                  </div>
          <div> 
              观众评：<span class="movie-info-average">{{movie.rating.average}}</span>
          </div>
          <div>
              主演：<span v-for="item in movie.casts" :key="item.id">{{item.name}}</span>
          </div>
          </div>
      </li>
  </ul>
  <div v-show="isEnd">
      <h3 class="end">数据到底了</h3>

  </div>
   <div class="loading" v-show="isLoading">
       <img src="@/assets/img/loading.gif" alt="">
   </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      movieList: [],
      isLoading: true,
      isEnd:false
    };
  },
  methods: {
    getData() {
      let url1 =
        "https://bird.ioliu.cn/v2?url=https://api.douban.com/v2/movie/in_theaters?start=0&count=5";
      let url2 = "https://api.myjson.com/bins/tll7o";
      this.isLoading=true;
      axios.get(url2).then(res => {
        // console.log(res.data.subjects);
          let getList = res.data.subjects.slice(
          this.movieList.length,
          this.movieList.length + 5
        );
        if(getList.length<5){
            this.isEnd=true;
        }
        this.movieList = this.movieList.concat(getList);
        this.isLoading = false;
      });
    }
  },
  beforeCreate() {},
  created() {
    this.$emit("switchTab", "movie");
    this.getData();
  },
  mounted() {
    window.onscroll = () => {
      let scrollTop = document.documentElement.scrollTop;
      let scrollHeight = document.documentElement.scrollHeight;
      let clientHeight = document.documentElement.clientHeight;

    //   console.log(scrollTop, scrollHeight, clientHeight);
      if (scrollHeight == scrollTop + clientHeight&&!this.isEnd) {
        this.getData();
      }
    };
  }
};
</script>
<style lang="scss" scoped>
.movie {
  padding: 0.2rem;
  border-bottom: 0.02rem;
  display: flex;
  &-img {
    flex-grow: 1;
    width: 0;
    img {
      width: 100%;
    }
  }
  &-info {
    margin-left: 0.2rem;
    width: 0;
    flex-grow: 3;
    &-title {
      color: #333;
      font-weight: 700;
      font-size: 0.34rem;
    }
    &-average {
      font-weight: 700;
      color: #faaf00;
    }

    &-star {
      color: #666;
      font-size: 0.26rem;
    }
  }
}
.loading {
  width: 3rem;
  text-align: center;
  position: fixed;
  bottom: 1rem;
  width: 100%;
}
.end{
    text-align: center;
}
</style>
