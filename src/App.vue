<template>
  <section class="score">
    
  </section>
  <section class="details">
    <h2 v-html="this.question"></h2>
    <input type="radio" name="options" value="true">
    <label for="true">True</label>
    
    <input type="radio" name="options" value="false">
    <label for="false">False</label>

    <button>Send</button>
  </section>
</template>

<script>
export default {
  name: 'App',

  //Function
  data() {
    return {
      question: undefined,
      incorrectAnswers: undefined,
      correctAnswers: undefined,
    }
  },

  computed: {
    answers() {
      var answers = JSON.parse(JSON.stringify(this.incorrectAnswers));
      answers.splice(Math.round(Math.random() * answers.length), 0, this.correctAnswers);
      return answers;
    }   
  }, 

  //Lifehooks cicle
  created() {
    this.axios
    .get('https://opentdb.com/api.php?amount=10&category=10')
    .then((response) => {
      this.question = response.data.results[0].question;
      this.incorrectAnswers = response.data.results[0].incorrect_answers;
      this.correctAnswers = response.data.results[0].correct_answer;
    })
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
  }
</style>
