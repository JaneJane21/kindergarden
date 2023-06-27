<template>
  <div class="comment-list-component">
    <my-button class="comment-btn"
               v-if="!displayAddRev"
               @click="showAdd">ОСТАВИТЬ ОТЗЫВ</my-button>
    <div v-else>
      <form @submit.prevent>
        <h2>Добавление отзыва</h2>
        <label for="name">Имя:</label>
        <input id="name" type="text" v-model="revName">
        <label for="review">Текст отзыва:</label>
        <textarea id="review" v-model="revBody"></textarea>
        <my-button class="add-btn" @click="addRev">ДОБАВИТЬ ОТЗЫВ</my-button>
      </form>
    </div>
    <div v-if="commentList.length>0" class="comment-list">
      <comment-item @addAnswer="addAnswer"
                    @deleteRev="this.$emit('deleteRev',comment)"
                    :status="status"
                    :comment="comment"
                    v-for="comment in commentList"
                    :key="comment.id">}
      </comment-item>
    </div>
    <div v-else>Отзывов пока нет</div>
  </div>

</template>

<script>
import CommentItem from "@/components/CommentItem";
import MyButton from "@/UI/MyButton";
export default {
  components: {MyButton, CommentItem},
  props:{
    commentList:{
      type:Array,
      default: ()=>[],
    },
    status:{
      type:Boolean,
      default:false
    }
  },
  data(){
    return{
      displayAddRev:false,
      revName:'',
      revBody:''
    }
  },
  methods:{
    showAdd(){
      this.displayAddRev = true
    },
    addRev(){
      this.displayAddRev = false
      this.$emit("addRev",{
        id:Date.now(),
        flag:'review',
        question:{
          date: new Date().getDate()+'.' +(new Date().getMonth() + 1)+'.' +new Date().getFullYear(),
          name:this.revName,
          body:this.revBody
        },
        answer:''
      })
      this.revBody = ''
      this.revName = ''
    },
    addAnswer(obj){
      this.$emit('addAnswer',obj)
    }

  }
}
</script>

<style scoped>
.comment-list-component{
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.comment-list{
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}
.comment-btn{
  background-color: white;
  border: 4px solid #FEF600;
  margin: 20px auto;
}
.comment-btn:hover{
  background-color: #FEF600;
  color: white;
  font-weight: 600;
}
form{
  display: flex;
  flex-direction: column;
  margin: 50px;
}
h2{
  text-align: center;
  margin-bottom: 10px;
}
/*form *{*/
/*  margin: 5px;*/
/*}*/
.add-btn{
  margin-top: 15px;
}
input,textarea{
  border: 1px solid rgb(53,45,45);
  border-radius: 8px;
  height: 25px;
  margin: 5px 0 8px 0;
  padding: 15px 8px;
}
textarea{
  height: 80px;
}
</style>