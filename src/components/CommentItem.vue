<template>
  <div class="comment-item">
    <div class="question">
      <div class="question-header">
        <p>{{comment.question.name}}</p>
        <p>{{comment.question.date}}</p>
      </div>
      <div>{{comment.question.body}}</div>
      <div v-if="status" class="q-btns">
        <my-button @click="deleteRev(comment)">Удалить отзыв</my-button>
        <my-button @click="showAnswer">Ответить</my-button>
      </div>
    </div>
    <div class="answer-form" v-if="displayAnswerForm">
      <textarea v-model="answerText"></textarea>
      <my-button @click="addAnswer(comment)">Добавить ответ</my-button>
    </div>
    <div v-if="comment.answer" class="answer">

        <div class="photo"><img src="../teacherPhoto.avif" alt="my photo"></div>
        <div class="answer-content">
          <div class="answer-content-header">
            <div>{{comment.answer.name}}</div>
            <div>{{comment.answer.date}}</div>
          </div>
          <div>{{comment.answer.body}}</div>
        </div>
    </div>
  </div>
</template>

<script>
import MyButton from "@/UI/MyButton";
export default {
  components: {MyButton},
  props:{
  comment:{
    type:Object
  },
  status:{
    type:Boolean,
    default: false
  }
},
  data(){
    return{
      displayAnswerForm:false,
      answerText:'',
  }
  },
  methods:{
    deleteRev(comment){
      this.$emit('deleteRev',comment)
    },
    showAnswer(){

      this.displayAnswerForm = true
    },
    addAnswer(comment){
      console.log(comment)
      console.log(this.answerText)
      let obj = {
        comment: comment,
        text: this.answerText
      }
      this.$emit('addAnswer',obj)
      this.displayAnswerForm = false
      this.answerText = ''

    }
  }
}
</script>

<style scoped>
.comment-item{
  width: 100%;
  margin: 25px auto;
}
.question{
  background-color: rgb(254,246,0);
  border-radius: 28px;
  padding: 30px;
  z-index: 1;
  position: relative;
}
.question-header{
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 20px;
}
.q-btns{
  display: flex;
  margin-top: 20px;
  align-items: center;
  justify-content: flex-end;
}
.q-btns *{
  border: none;
  background-color: white;
  cursor: pointer;
  margin: 0 18px;
}
.answer,.answer-form{
  background-color: #FFF;
  border-radius: 0 0 28px 28px;
  padding: 70px 30px 30px 30px;
  margin-top: -30px;
  display: flex;
}
.answer-form{
  align-items: center;
  flex-direction: column;

}
/*.answer{*/
/*  width: 100%;*/
/*  position: relative;*/
/*}*/
textarea{
  width: 100%;
  height: 80px;
  border: 1px solid rgb(53,45,45);
  border-radius: 8px;
  padding: 20px;
  margin: 10px;
}
/*.photo{*/

/*}*/
/*.photo img{*/
/*  width: 80px;*/
/*  height: 100%;*/
/*  border-radius: 50%;*/
/*  object-fit: cover;*/

/*}*/
.photo {
  width: 80px;
  height: 80px;

}

.photo img {
  border-radius: 50%;
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: 0 0;
}
.answer-content{
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: 100%;
  margin-left: 20px;
  justify-content: center;

}
.answer-content-header{
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  margin-bottom: 10px;
}
</style>