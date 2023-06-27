<template>
  <div class="portf-elem">
    <div class="img-box">
      <img :src="portfItem.image" alt="diploma">
    </div>
    <p>{{portfItem.text}}</p>
  </div>
</template>

<script>
export default {
  props:{
    portfItem:{
      type:Object
    }
  }
}
</script>

<style scoped>
.portf-elem{
  display: flex;
  flex-direction: column;
  width: 35%;
  height: auto;
  margin: 25px 0px;
  align-items: center;
  justify-content: flex-start;

}
.img-box{
  width:80%;
  height: auto;
  margin-bottom: 15px;
  /*object-fit: contain;*/
}
img{
  width: 100%;
  /*height: auto;*/
  object-fit: contain;
}
p{
  text-align: center;
}
</style>