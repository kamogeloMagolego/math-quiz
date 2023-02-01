<template>
  <div>
    <div v-if="quizStarted">
      <h5>Hi {{ name }}! here is your score: wins {{ wins }} & losses {{ losses }}</h5>
      <h4>{{ aperentLeft }} {{ operator }} {{ aperentRight }}</h4>
      <button
        @click="selectAnswer(answer)"
        v-for="(answer, index) of answers"
        :key="index"
      >
        {{ answer }}
      </button>
    </div>
    <div v-if="!quizStarted">
      <button @click="startQuiz">Start</button>
    </div>
    <button @click="$emit('onBack')">Back</button>
  </div>
</template>

<script>
export default {
  name: "MathQuiz",
  props: ["operator", "name"],
  data() {
    return {  
      quizStarted: false,
      wins: 0,
      losses: 0,
      aperentLeft: null,
      aperentRight: null,
      answers: [],
      expectedAnswer: null,
    };
  },
  methods: {
    startQuiz() {
      this.quizStarted = true;
      this.aperentLeft = parseInt(Math.random() * 13);
      this.aperentRight = parseInt(Math.random() * 13);

      const methods = {
        "+": (a, b) => a + b,
        "-": (a, b) => a - b,
        "/": (a, b) => a / b,
        "*": (a, b) => a * b,
      };

      this.answers = [];
      const methodToUse = methods[this.operator];

      for (let i = 0; i < 5; i++) {
        const answer = methodToUse(
          parseInt(Math.random() * 3 + 5),
          parseInt(Math.random() * 3+3)
        );
        this.answers.push(answer);
        console.log(this.answers);
      }
      const expected = methodToUse(this.aperentLeft, this.aperentRight);
      this.answers[parseInt(Math.random() * this.answers.length)] = expected;
      // this.answers[parseInt(Math.random() * this.answers.length)] = expected;
      // this.answers[parseInt(Math.random() * this.answers.length)] = expected;
      // this.answers[parseInt(Math.random() * this.answers.length)] = expected;
      // this.answers[parseInt(Math.random() * this.answers.length)] = expected;
      this.expectedAnswer = expected;
      console.log(this.expectedAnswer);
    },
    selectAnswer(answerSelected) {
      if (answerSelected === this.expectedAnswer) {
        this.wins++;
        this.startQuiz();
      } else {
        alert("wrong answer");
        this.losses++;
        this.startQuiz();
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style></style>
