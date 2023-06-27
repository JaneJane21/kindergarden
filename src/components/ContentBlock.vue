<template>
  <div class="main-block">
    <div class="header">
      <h3>{{title}}</h3>
      <div class="line"></div>
    </div>
  <div class="content">
    <slot></slot>
  </div>

  </div>
</template>

<script>
export default {
props:{
  title:{
    type:String,
    default:'Заголовок страницы'
  }
}
}
</script>

<style scoped>
.line{
  background-color: rgb(254,246,0);
  height: 5px;
  width: 100%;
  margin-top: 5px;
}
.main-block{
  width: 70%;
  margin: 60px auto;
}
.header{
  width: 45%;
  margin: 60px 0;
}
</style>