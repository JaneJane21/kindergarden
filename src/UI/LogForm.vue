<template>
  <div>
    <form @submit.prevent>
      <h2>Авторизация</h2>
      <label for="login">Логин:</label>
      <input id="login" type="text" v-model="login">
      <label for="pswrd">Пароль:</label>
      <input id="pswrd" type="password" v-model="pswrd">
      <my-button class="log-btn" @click="logIn">ВОЙТИ</my-button>
    </form>
  </div>
</template>

<script>
import MyButton from "@/UI/MyButton";
export default {
  components: {MyButton},
  data(){
    return{
      login:'',
      pswrd:''
  }
  },
  methods:{
    logIn(){
      this.$emit('logUser',{login:this.login,password:this.pswrd})
    }
  }
}
</script>

<style scoped>
form{
  display: flex;
  flex-direction: column;
  margin: 50px;
}
h2{
  text-align: center;
}
form *{
  margin: 4px;
}
.log-btn{
  margin-top: 15px;
}
input{
  border: 1px solid rgb(53,45,45);
  border-radius: 8px;
  height: 25px;
  padding: 15px 8px;
}
</style>