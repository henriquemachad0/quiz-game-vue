<template>
  <div>
    <template v-if="this.question">

      <h1 v-html="this.question"></h1>

      <template v-for="(answer, index) in this.answers" :key="index">
        <input 
        type="radio" 
        name="options" 
        :value="answer"
        v-model="this.chosen_answer">

        <label v-html="answer"></label><br>
      </template>

      <button @click="this.submitAnswer()" class="send" type="button">Confirmar</button>

    </template>

  </div>
</template>

<script>

export default {
  name: 'App',

  data(){
    return {
      question: undefined,
      incorrectAnswers: undefined,
      correctAnswer: undefined,
      chosen_answer: undefined
    }
  },
  methods:{
    submitAnswer() {
      if(!this.chosen_answer){
        alert('Escolha uma das opções')
      } else {
        if(this.chosen_answer == this.correctAnswer){
          alert('Você acertou')
        } else {
          alert('Você errou')
        }
      }
    }
  },
  computed: {
    answers() {
      var answers = JSON.parse(JSON.stringify(this.incorrectAnswers))
      answers.splice(Math.round(Math.random() * answers.length), 0, this.correctAnswer)
      return answers
    }
  },
  created(){
    this.axios
    .get('https://opentdb.com/api.php?amount=1&category=18')
    .then((response) => {
      this.question = response.data.results[0].question
      this.incorrectAnswers = response.data.results[0].incorrect_answers
      this.correctAnswer = response.data.results[0].correct_answer
    })
  }
}

</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  max-width: 960px;

  input[type=radio] {
    margin: 12px 4px;
  }

  button.send {
    margin-top: 12px;
    height: 40px;
    min-width: 120px;
    padding: 0 16px;
    color: #fff;
    background-color: #1867c0;
    border: 1px solid #1867c0;
    cursor: pointer;
  }
}
</style>
