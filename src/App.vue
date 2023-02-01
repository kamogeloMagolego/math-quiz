<template>
  <div>
    <h1 v-if="!english">Math Quiz App</h1>
    <input
      v-if="!operator"
      v-model="name"
      type="text"
      placeholder="enter name"
      :class="error ? '' : error"
    />
    <math-quiz
      :name="name"
      @onBack="clearOperator"
      v-if="operator ? !english : operator"
      :operator="operator"
    ></math-quiz>
    <selected-question
      v-if="!operator "
      @changeOperator="selectOperator"
    ></selected-question>
    <english-quiz v-if="english" :english="english" :operator="operator"></english-quiz>
    <button v-if="!operator" @click="openEnglish">Start English Quiz</button>
  </div>
</template>

<script>
import MathQuiz from "./components/MathQuiz.vue";
import SelectedQuestion from "./components/SelectedQuestion.vue";
import EnglishQuiz from './components/EnglishQuiz.vue';

export default {
  name: "App",
  components: {
    MathQuiz,
    SelectedQuestion,
    EnglishQuiz
  },
  data() {
    return {
      operator: null,
      name: "",
      // maths: false,
      english: false
    };
  },
  methods: {
    selectOperator(operator) {
      // this.operator = operator;
      if(this.name){
        this.operator = operator
      } else{
        return
      }
    },
    clearOperator() {
      this.operator = null;
    },
    openEnglish(){
      this.english = true;
      this.operator = !this.operator
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-size: 35px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
button {
  height: 80px;
  cursor: pointer;
  padding: 10px;
  width: 160px;
  background-color: #42b983;
  color: white;
  margin: 5px;
  font-size: 24px;
  vertical-align: top;
  border: #42b983;
}
input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 20px;
  margin-right: auto;
  margin-left: auto;
  border: 1px solid #42b983;
}
.error{
  background-color: #f80000;
}
</style>
