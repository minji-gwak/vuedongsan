<template>
  <div class="black-bg" v-if="detail == true">
    <div class="white-bg">
      <h4>원룸들 </h4>
      <p>상세페이지 내용임</p>
      <button @click="detail = false">X</button>
    </div>
  </div>


  <div id="common_header" :class="{original_header: scrollPosition < 100, change_header: scrollPosition >= 100}">
    <a v-for="a in menus" :key="a">{{ a }}</a>
  </div>

  <div style="height: 60px"></div>
  
  <div v-for="(a,i) in oneroom" :key="i">
    <img :src="oneroom[i].image" class="room-img">
    <h4 @click="detail = true">{{ oneroom[i].title }}</h4>
    <p>{{ oneroom[i].content }}</p>
    <p>{{ oneroom[i].price }} 원</p>
    <!-- 
    <button @click="increase(i)">허위매물신고</button> <span> 신고 수 : {{ reports[i] }}</span>
    -->
  </div>

</template>

<script>
import oneroomData from './assets/oneroom.js';



export default {
  name: 'App',
  data(){
    return{
      oneroom : oneroomData,
      images : [require("./assets/room0.jpg"), require("./assets/room1.jpg"), require("./assets/room2.jpg")],
      reports : [0, 0, 0],
      menus : ['Home', 'Products', 'About'],
      products : ['역삼동원룸', '천호동원룸','마포구원룸'],
      price : ['50', '70', '가격 문의'],
      scrollPosition : null,
      detail : false,
    }
  },
  methods : {
    increase(i){
      this.reports[i]++
    },
    scrollHeader(){
      this.scrollPosition = window.scrollY
    },

  },
  
  mounted() {
    window.addEventListener('scroll', this.scrollHeader);
  },

  components: {
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  margin: 0;
}

div {
  box-sizing: border-box;
}

#common_header {
  position: fixed;
  width: 100%;
  padding: 15px;
}
.original_header {
  background: darkslateblue;
  color: white;
}
.change_header {
  background: white;
  border-bottom: 1px solid #d3d3d354;
  box-shadow: 0px 0.1px 5px 0.1px #e7e7e7;
}

#common_header a {
  padding: 10px;
}

.room-img {
  width: 90%;
  margin-top: 40px;
}

.black-bg {
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  margin-top: 10%;
  padding: 20px;
}
</style>