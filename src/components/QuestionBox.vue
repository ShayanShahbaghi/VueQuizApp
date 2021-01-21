<template>
  <div class="qBox shadow">
      <h3 class="qTitle">
          {{
              this.question.title
          }}
      </h3>
      <div class="answersBox">
          <div v-for="index in this.question.answers.length" :key="index" :class="getSelectedClass(index - 1)" @click="selectAnswer(index - 1)">
              {{
                  question.answers[index - 1].title
              }}
          </div>
      </div>
      <div class="buttons" dir="rtl">
          <div class="next" :disabled="index == 9" @click="nextQuestion()">
              Next
          </div>
          <div class="prev" :disabled="index == 0" @click="prevQuestion()">
              Prev
          </div>
      </div>
  </div>
</template>

<script>
export default {
    props: {
        question: Object,
        selectAnswer: Function,
        index: Number,
        nextQuestion: Function,
        prevQuestion: Function
    },
    methods: {
        getSelectedClass(index){
            if (this.question.selected != index){
                return 'answer shadow'
            } else {
                return 'answer shadow selected'
            }
        }

    }
}
</script>

<style>
.qBox {
    margin: 8% auto;
    padding: 2%;
    border-radius: 5px;
    width: 40%;
}
.answersBox {
    margin: 30px 0 0 ;
}
.answer {
    width: 80%;
    margin: 10px auto;
    padding: 15px;
    cursor: pointer;
    border-radius: 5px;
}
.selected {
    background-color: #1abc9c;
    color:white;
}
.buttons {
    margin: 30px auto 0;
    width: 50%;
}
.next {
    display: inline-block;
    background-color: #3498db;
    color: white;
    padding: 10px 25px;
    border-radius: 5px;
    margin-left: 10px;
    cursor: pointer;
}
.prev {
    display: inline-block;
    background-color: #e74c3c;
    color: white;
    padding: 10px 25px;
    border-radius: 5px;
    cursor: pointer;
}
</style>