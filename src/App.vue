<template>
  <section class="score">
    
  </section>
  <section class="details">
    <h2>Lorem ipsum dolor sit amet consectetur adipisicing elit. Illum sed, iste, deleniti, aperiam cumque repellendus hic nobis maxime inventore magni earum! Dolorum fuga dolore perferendis voluptates molestias voluptate quia doloremque.</h2>
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

  created() {
    this.axios
    .get('https://opentdb.com/api.php?amount=10&category=10')
    .then((response) => {
      console.log(response.data.results[0])
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
