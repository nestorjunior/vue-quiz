<template>
  
  <section class="score">
    <ScoreBoard :winCount='this.winCount' :loseCount='this.loseCount' />
  </section>

  <template v-if="this.question">
    <section class="details">
      <h2 v-html="this.question"></h2>

      <template v-for="answer in this.answers" :key="answer">
        <section class="general-box">
          <input 
            :disabled="this.answerSubmitted"
            type="radio" 
            name="options" 
            :value="answer"
            v-model="chosenAnswer">
          
          <label class="item-answer" v-html="answer"></label>
        </section>  
      </template>

      <button class="send" @click="this.submitAnswer" v-if="!this.answerSubmitted">Send</button>
    </section>
    <section class="result" v-if="this.answerSubmitted">
      <h4 v-if="this.chosenAnswer == this.correctAnswers">
        &#9989; Congrats, the answer <strong>{{ this.correctAnswers }} </strong>is correct!.
      </h4>
      <h4 v-else>
        &#10060; I'm sorry, you picked the wrong answer: {{ this.chosenAnswer }}.
      </h4>

      <button @click="this.getNewQuestion()" class="send">Next Question</button>
    </section>
  </template>
</template>

<script>
import ScoreBoard from '@/components/ScoreBoard.vue';

export default {
  name: 'App',
  components: {
    ScoreBoard
  },

  //Function
  data() {
    return {
      question: undefined,
      incorrectAnswers: undefined,
      correctAnswers: undefined,
      chosenAnswer: undefined,
      answerSubmitted: false,
      winCount: 0,
      loseCount: 0,
    }
  },

  computed: {
    answers() {
      var answers = JSON.parse(JSON.stringify(this.incorrectAnswers));
      answers.splice(Math.round(Math.random() * answers.length), 0, this.correctAnswers);
      return answers;
    }   
  }, 

  methods: {
    submitAnswer() {
      if (!this.chosenAnswer) {
        alert("Pick one the options")
      } else {
        this.answerSubmitted = true;
        if (this.chosenAnswer == this.correctAnswers) {
          this.winCount++;
        } else {
          this.loseCount++;
        }
      }
    },

    getNewQuestion() {
      //Resetando os campos
      this.answerSubmitted = false;
      this.chosenAnswer = undefined;
      this.question = undefined;

      this.axios
      .get('https://opentdb.com/api.php?amount=10&category=10')
      .then((response) => {
        this.question = response.data.results[0].question;
        this.incorrectAnswers = response.data.results[0].incorrect_answers;
        this.correctAnswers = response.data.results[0].correct_answer;
      })  
    }

  },

  //Lifehooks cicle
  created() {
    this.getNewQuestion();
  },
}

//Api URL: https://opentdb.com/api.php?amount=10&category=10
</script>

<style lang="scss">
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;

    button {
      display: block;
      margin: 10px auto;
      padding: 15px 25px;
      cursor: pointer;
      min-width: 120px;
      color: #fff;
      background-color: #1867c0;
      border: #1867c0;
      border-radius: 5px;
      &:hover {
        background-color: #145cad;
      }
    }

    .general-box {
      display: flex;
      padding: 15px;
    }

    .details {
      display: inline-block;
      width: 650px;
      text-align: left;
    }

  }
</style>
