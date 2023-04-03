<template>

  <transition name="fade">
    <ModalUi :oneroom = "oneroom" :clIdx = "clIdx" :modalIsOpen = "modalIsOpen" @closeModal="modalIsOpen = false"></ModalUi>
  </transition>
  
  <nav>
      <a v-for="(data) in menu" :key = "data" href="#">{{data}}</a>
  </nav>
  <DisCount></DisCount>
  <button @click="priceSort">가격순 정렬</button>
  <button @click="sortBack">되돌리기</button>
  <!-- object -->
  <CardUi :oneroom = "oneroom" @openModal="modalIsOpen = true; clIdx = $event;"></CardUi>

  
  <!-- <div v-for="(room,i) in oneroom" :key="room">
    <img :src="oneroom[i].image" class='room-img' alt="">
    <h4 @click="modalIsOpen = true; clIdx = i">{{oneroom[i].title}}</h4>
    <p></p>
    <p>{{oneroom[i].price}}원</p>
  </div> -->
  <!-- <div>
    <img :src="oneroom[0].image" class='room-img' alt="">
    <h4 @click="modalIsOpen = true">{{oneroom[0].title}}</h4>
    <p>{{oneroom[0].price}}원</p>
    <button @click="increase(0)">허위매물신고</button> <span>신고수 : {{countNum[0]}}</span>
  </div>
  <div>
    <img src="./assets/room1.jpg" class='room-img' alt="">
    <h4>{{products[1]}}</h4>
    <p>50만원</p>
    <button @click="increase(1)">허위매물신고</button> <span>신고수 : {{countNum[1]}}</span>
  </div>
  <div>
    <img src="./assets/room2.jpg" class='room-img' alt="">
    <h4>{{products[2]}}</h4>
    <p>50만원</p>
  </div>
  <button @click="increase(2)">허위매물신고</button> <span>신고수 : {{countNum[2]}}</span> -->
</template>

<script>
// 원룸정보 가져오기
import data from './oneroom.js';
import Discount from './Discount.vue';
import ModalUi from './Modal';
import CardUi from './Card.vue';


export default {
  name: 'App',
  data(){
    return{
      // 데이터 사본 
      original_oneroom : [...data], 
      oneroom : data,
      clIdx: 0,
      modalIsOpen : false,
      countNum : [0,0,0],
      menu : ['HOME', 'ABOUT', 'PRODUCTS'],
      products: ['역삼동원룸', '천호동원룸', '마포구원룸'],
      random: '가격은 아무거나',
      soyoung : {name: 'soyoung', age: 27},
      //showDiscount : true,
    }
  },
  methods : {
    increase(index){
      this.countNum[index]++;
    },
    sortBack(){
      this.oneroom = [...this.original_oneroom];
    },
    priceSort(){
      this.oneroom.sort(function(a, b){
        return a.price - b.price
      })
      // array.sort(function(a,b){
      //   return a - b
      // });
    }
  },
  // life cycle hooks
  mounted(){
    //마운트 되고 나서 코드 실행 2초 뒤에 discount 창 없애기.
    // setTimeout(()=>{
    //   this.showDiscount = false;
    // }, 2000);

  },
  components: {
    DisCount: Discount,
    ModalUi : ModalUi,
    CardUi: CardUi,
  }
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
/* .start{
  opacity:0;
  transition: all 1s;
}
.end{
  opacity:1;
} */

.fade-enter-from{
  /* 시작 */
  opacity:0;
  transform:translateY(-10%);
}
.fade-enter-active{
  transition: all 1s;
}
.fade-enter-to{
  /* 끝 */
  opacity:1;
  transform:translateY(0%);
}
.fade-leave-from{
  /* 시작 */
  opacity:1;
}
.fade-leave-active{
  transition: all 0.5s;
}
.fade-leave-to{
  /* 끝 */
  opacity:0;
}

nav{
  background: darkslateblue;
  padding:15px;
  border-radius: 5px;
}
nav a{
  color:#fff;
  padding: 10px;
  text-decoration: none;
}
.room-img{
  width: 100%;
  margin-top: 40px;
}
.black-bg{
  width:100%;
  height:100%;
  background: rgba(0,0,0,0.5);
  position:fixed;
  padding: 20px;
}
.white-bg{
  width:100%;
  background: white;
  border-radius: 8px;
  padding:20px;
}
.close{
  position:absolute;
  top:10%;
  right: 10%;
  cursor:pointer;
}
h4{
  cursor:pointer;
}
.discount{
  background: #eee;
  padding: 10px;
  margin:10px;
  border-radius: 5px;
}
.discount > h4{
  cursor:auto;
}
</style>
