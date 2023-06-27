<template>
  <div class="header">
    <div class="logo"><img alt="logo" src="../logo.jpg"></div>
    <div class="content">
      <div class="info bold">ПЕРСОНАЛЬНЫЙ САЙТ ВОСПИТАТЕЛЯ<br>АННЕНКО АНГЕЛИНА ВИТАЛЬЕВНА</div>
      <div class="line"></div>
      <ul>
        <li @click="$emit('changePage','me')">О СЕБЕ</li>
        <li @click="$emit('changePage','portfolio')">ПОРТФОЛИО</li>
        <li @click="$emit('changePage','toparents')">РОДИТЕЛЯМ</li>
      </ul>
    </div>
    <my-button v-if="!currentUser" @click="this.$emit('update:display',true)" class="log-btn bold">ВОЙТИ</my-button>
    <my-button v-else @click="this.$emit('update:currentUser',false)" class="log-btn bold">ВЫЙТИ</my-button>
  </div>
</template>

<script>
import MyButton from "@/UI/MyButton";
export default {
  components: {MyButton},
  props:{
  display:{
    type:Boolean,
    default:false
  },
  currentUser:{
    type:Boolean,
    default: false
  }
}
}
</script>

<style scoped>
.header{
  display: flex;
  width: 100%;
  height: 130px;
  align-items: center;
  justify-content: space-between;
  padding: 0 40px;
  background-color: white;
  margin: 40px auto;
}
.logo{
  object-fit: cover;
}
.line{
  background-color: rgb(255,253,199);
  height: 7px;
  width: 100%;
}
.content *{
  margin: 5px auto;
}
.content{
  display: flex;
  width: 80%;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;

}
.info{
  text-align: center;
}
ul{
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  width: 100%;
  list-style-type: none;
}
li{
  text-decoration: none;
}
li:hover{
  text-decoration: underline;
  cursor: pointer;
}
.log-btn{
  border: none;
  background-color: white;
  cursor: pointer;
  align-self: flex-start;
  margin-top: 15px;
}
.log-btn:hover{
  text-decoration: underline;
  background-color: white;
  color: black;
}
.bold{
  font-weight: 600;

}
</style>