<template>
  <div class="hello">


  <div v-for="(joke, index) in jokes" :key="index" class="text item jokes Aligner">
    <el-card class="box-card">
    <li>
      {{joke.joke}}
    </li>
</el-card>
  </div>


  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'HelloWorld',
  data() {
    return {
      jokes: []
    }
  },
  methods: {
    getJokes: function () {
      axios.get('https://icanhazdadjoke.com/search', {
         headers: {
          Accept: 'application/json'
        },
        params: {
          limit: 300
        }
      })
      .then((result) => {
        console.log(result.data.results)
        this.jokes = result.data.results
      }).catch((err) => {
        console.log(err)
      });
    },
  },
  created : function () {
    this.getJokes()
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.jokes{
  display: flex
}
.item {
    padding: 18px 0;
    list-style: none;
  }
  .text {
    font-size: 25px
  }
  .Aligner {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
