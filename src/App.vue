<template>
  <div id="app">
    <Header :questionNumber="this.index + 1"/>
    <QuestionBox 
    :question="this.questions[this.index]" 
    :selectAnswer="this.selectAnswer" 
    :index="this.index"
    :nextQuestion="this.nextQuestion"
    :prevQuestion="this.prevQuestion"
    />
  </div>
</template>

<script>
import Header from './components/Header'
import QuestionBox from './components/QuestionBox'
export default {
  name: 'App',
  components: {
    Header,
    QuestionBox
  },
  data(){
    return {
      questions:[],
      index:0
    }
  },
  created(){

    var requestOptions = {
      method: 'GET',
      redirect: 'follow'
    };

    fetch("https://opentdb.com/api.php?amount=10&category=18&difficulty=hard&type=multiple", requestOptions)
      .then(response => response.text())
      .then(result => this.handleRequest(result))
      .catch(error => console.log('error', error));
  },
  methods: {
    handleRequest(result){
      this.parseJsonToNewObjects(JSON.parse(result)['results'])
    },
    // here we want to create new object using json
    parseJsonToNewObjects(questions){
      var questionsArray = []
      console.log(questions.length)
      for (var i = 0; i < questions.length;i++){
        const question = questions[i]
        console.log(question)
        var answers = question.incorrect_answers
        console.log(answers)
        const trueAnswer = question.correct_answer
        answers = answers.map(answer => ({
          title: answer,
          status: false
        }))
        answers.push({title: trueAnswer,status:true})
        answers.sort(() => Math.random() - 0.5);
        questionsArray.push(
          {
            title: question.question,
            answers: answers,
            selected: null
          }
        )
      }
      this.questions = questionsArray
    },
    selectAnswer(answerIndex){
      this.questions[this.index].selected = answerIndex
    },
    nextQuestion(){
      if (this.index != 9){
        this.index += 1
      }
    },
    prevQuestion(){
      if (this.index != 0){
        this.index -= 1
      }
    }
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
</style>
