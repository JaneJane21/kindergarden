<template>
  <div class="container">
<!--    <button @click="reg">reg</button>-->
    <my-window v-model:display="displayLog">
      <log-form @logUser="logUser"></log-form>
    </my-window>
    <my-header v-model:currentUser="activeUserBool"
               v-model:display="displayLog"
               @changePage="selectTab"></my-header>
    <content-block :title="titleMe" v-if="displayMe">
      <about-me></about-me>
    </content-block>
    <content-block :title="titlePortfolio"
                   v-if="displayPortfolio">
      <my-portfolio :portfList="portfolioList"></my-portfolio>
    </content-block>
    <content-block :title="titleToParents"
                   v-if="displayToParents">
      <my-select v-model="selectedSort" :options="options"></my-select>
      <comment-list @addAnswer="addAnswer"
                    @deleteRev="deleteRev"
                    :status="activeUserBool"
                    @addRev="addReview"
                    :commentList="sortComment">
      </comment-list>
    </content-block>
  </div>
</template>

<script>

import MyHeader from "@/components/MyHeader";
import ContentBlock from "@/components/ContentBlock";
import AboutMe from "@/components/AboutMe";
import MyPortfolio from "@/components/MyPortfolio";
import MyWindow from "@/UI/MyWindow";
import LogForm from "@/UI/LogForm";
import CommentList from "@/components/CommentList";
import MySelect from "@/UI/MySelect";
export default {
  name: 'App',
  components: {MySelect, CommentList, LogForm, MyWindow, MyPortfolio, AboutMe, ContentBlock, MyHeader},
  data(){
    return{
      titleMe:'Давайте знакомиться!',
      titlePortfolio:'Мои достижения',
      titleToParents:'Оставьте свои пожелания и замечания',

      displayMe:true,
      displayPortfolio:false,
      displayToParents: false,
      displayLog:false,


      activePage:'',
      downloadFile:'',
      activeUser:'',
      activeUserBool:false,
      comments:[],

      selectedSort:"none",
      options:[
        {value:'new',name:'Сначала новые'},
        {value:'old',name:'Сначала старые'},
      ],


      portfolioList:[
        {id:0, image:'https://nsportal.ru/sites/default/files/portfolio_photos/2015/11/22/2015-09-13-0016.jpg',text:'Инновационные разработки в коррекции речевых нарушений'},
        {id: 1, image: 'https://nsportal.ru/sites/default/files/portfolio_photos/2015/11/22/2015-09-13-0017.jpg',text: 'Проведение областного мероприятия по теме "Использование компьютерных технологий в коррекции речевых нарушений у детей'},
        {id:2, image: 'https://nsportal.ru/sites/default/files/portfolio_photos/2015/11/22/2015-09-13-0020.jpg', text:'Общероссийский конкурс "Парнас: Применяем ИКТ в ДОУ-3". Разработка презентации урока (занятия) "Союз а"'},
        {id:3, image: 'https://nsportal.ru/sites/default/files/portfolio_photos/2015/11/22/2015-09-13-0010.jpg', text:'Участник семинара "Использование интерактивной доски и документ-камеры при обучении дошкольников'},
      ]
    }
  },
  methods:{
    selectTab(str){
      if(str==='me'){
        this.displayPortfolio = false
        this.displayToParents = false
        this.activePage = 'me'
        this.displayMe = true
      }
      else if(str==='portfolio'){
        this.displayMe = false
        this.displayToParents = false
        this.activePage = 'portfolio'
        this.displayPortfolio = true
      }
      else{
        this.displayMe = false
        this.displayPortfolio = false
        this.activePage = 'toparents'
        this.displayToParents = true
      }
    },
    // savingDoc(str){
    //   console.log(str)
    //   this.portfolioList.push({id:Date.now(),image: str,text: 'blbablalblab'})
    // },
    logUser(data){
      let user
      for(let i=0; i<localStorage.length;i++){
        let key = localStorage.key(i)
        let item = localStorage[key]
        let currentUser = JSON.parse(item)
        if(data.login===currentUser.login && data.password === currentUser.password){
          user = currentUser
        }
      }
      if(!user){
        alert('Ошибка авторизации')
      }
      else {
        this.activeUser = user
        this.activeUserBool = true
        this.displayLog = false

      }
    },
    addReview(comment){
      localStorage.setItem(Date.now(),JSON.stringify(comment))
      this.comments.length = 0
      for(let i=0; i<localStorage.length;i++){
        let key = localStorage.key(i)
        let item = JSON.parse(localStorage[key])
        if(item.flag === 'review'){
          this.comments.push(item)
        }
      }
    },
    // reg(){
    //   let user = {login:'teacher', password:'0000',name:'Анненко Ангелина Витальевна'}
    //   localStorage.setItem('123456789',JSON.stringify(user))
    // },
    deleteRev(comment){
      this.comments = this.comments.filter(com => com.id!==comment.id)
      for (let i=0; i<localStorage.length;i++){
        let key = localStorage.key(i)
        let item = JSON.parse(localStorage[key])
        if(item.id === comment.id){
          localStorage.removeItem(key)
        }
      }
    },
    addAnswer(obj){
      let searchID = obj.comment.id
      let item
      for (let i=0; i<localStorage.length;i++){
        let key = localStorage.key(i)
        item = JSON.parse(localStorage[key])
        if(item.id === searchID){
          item.answer = {
            date: new Date().getDate()+'.' +(new Date().getMonth() + 1)+'.' +new Date().getFullYear(),
            name:'Анненко Ангелина Витальевна',
            body:obj.text
          }
          localStorage.setItem(key,JSON.stringify(item))
        }
      }
      this.comments.length = 0
      for(let i=0; i<localStorage.length;i++){
        let key = localStorage.key(i)
        let item = JSON.parse(localStorage[key])
        if(item.flag === 'review'){
          this.comments.push(item)
        }
      }
    }
  },
  computed:{
    sortComment(){
      if (this.selectedSort === "old"){
        console.log([...this.comments].sort((p1,p2)=>(p1.id-p2.id)))
        return [...this.comments].sort((p1,p2)=>(p1.id-p2.id))
      }
      else if(this.selectedSort === "new"){
        return [...this.comments].sort((p1,p2)=>(p1.id-p2.id)).reverse()
      }
      else return this.comments
    }
  },
  mounted() {
    for(let i = 0; i< localStorage.length; i++){
      let key = localStorage.key(i)
      let item = JSON.parse(localStorage[key])
      if(item.flag === 'review'){
        this.comments.push(item)
      }
    }
  }

}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Raleway:wght@400;600&display=swap");
*{
  box-sizing: border-box;
  font-family: 'Raleway', sans-serif;
  padding: 0;
  margin: 0;
  color: rgb(53,45,45);
}

</style>
