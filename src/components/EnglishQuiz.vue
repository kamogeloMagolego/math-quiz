<template>
  <main class="app">
    <h1>English Quiz</h1>
    <section class="quiz" v-if="!quizCompleted">
      <div class="quiz-info">
        <span class="question">{{ getCurrentQuestion.question }}</span>
        <!-- <span class="score">Score {{ score }} / {{ questions.length }}</span> -->
      </div>
      <div class="options">
        <labels
          v-for="(option, index) in getCurrentQuestion.options"
          :key="index"
          :class="`option ${
            getCurrentQuestion.selected == index
              ? index == getCurrentQuestion.answer
                ? 'correct'
                : 'wrong'
              : ''
          } ${
            getCurrentQuestion.selected != null &&
            index != getCurrentQuestion.selected
              ? 'disabled'
              : ''
          }`"
        >
          <input
            type="radio"
            :name="getCurrentQuestion.index"
            :value="index"
            v-model="getCurrentQuestion.selected"
            :disabled="getCurrentQuestion.selected"
            @change="setAnswer"
          />
          <span>{{ option }}</span>
        </labels>
      </div>
      <button @click="nextQuestion" :disabled="!getCurrentQuestion.selected">
        {{
          getCurrentQuestion.index == questions.length - 1
            ? "Finish"
            : getCurrentQuestion.selected == null
            ? "Select An Option"
            : "Next Question"
        }}
      </button>
    </section>
    <section v-else>
      <h2>You have finished the English Quiz</h2>
      <p>Your score is {{ score }}/{{ questions.length }}</p>
    </section>
  </main>
</template>

<script setup>
import { computed, ref } from "vue";
const questions = ref([
  {
    question: "what is a verb?",
    answer: 0,
    options: ["A doing Word", "An Ice-Cream Maker", "Name of a person"],
    selected: null,
  },
  {
    question:
      "_____ did you live in New York? B: I lived there for almost five years.",
    answer: 2,
    options: ["How much", "When", "How long"],
    selected: null,
  },
  {
    question: "When ____?",
    answer: 1,
    options: ["did you arrived", "did you arrive", "were you arrived"],
    selected: null,
  },
  {
    question: "They threw a rock _____ the window and broke the glass.",
    answer: 0,
    options: ["through", "across", "into"],
    selected: null,
  },
  {
    question:
      "He didn't speak English, _____ it was difficult to make him understand what he had to do..",
    answer: 1,
    options: ["although", "because", "so"],
    selected: null,
  },
  {
    question:
      "Why did you turn off the TV? B: Because I _____. I'm very tired.",
    answer: 2,
    options: ["go to sleep", "will go to sleep", "'m going to sleep"],
    selected: null,
  },
  {
    question: "When will Lucy arrive?",
    answer: 0,
    options: ["At 7 PM", "No, she won't", "From France "],
    selected: null,
  },
  {
    question: "Who called here so late?",
    answer: 1,
    options: ["It's midnight", "It was Ryan", "Yes, I called"],
    selected: null,
  },
  {
    question: "Do you want to watch a movie?",
    answer: 2,
    options: ["At the cinema", "Yes, I watched it", "No, I don't "],
    selected: null,
  },
  {
    question: "Have you done the laundry?",
    answer: 2,
    options: [" Yes, I do", "On Wednesdays", "No, I haven't"],
    selected: null,
  },
]);

const quizCompleted = ref(false);
const currentQuestion = ref(0);
const score = computed(() => {
  let value = 0;
  console.log(score, getCurrentQuestion, setAnswer, nextQuestion);
  questions.value.map((q) => {
    if (q.selected == q.answer) {
      value++;
    }
  });
  return value;
});
const getCurrentQuestion = computed(() => {
  let question = questions.value[currentQuestion.value];
  question.index = currentQuestion.value;
  // console.log(question.index);
  return question;
});
const setAnswer = (e) => {
  questions.value[currentQuestion.value].selected = e.target.value;
  e.target.value = null;
};
const nextQuestion = () => {
  if (currentQuestion.value < questions.value.length - 1) {
    currentQuestion.value++;
  } else {
    quizCompleted.value = true;
  }
};
// const getSetAnswer = setAnswer;
</script>

<style scoped>
.question {
  font-size: 2rem;
}
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;
  min-height: 100hv;
}
.quiz {
  padding: 1rem;
  width: 100%;
  max-width: 640px;
}
.quiz-info {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}
.options {
  margin-bottom: 1rem;
}
.option {
  display: block;
  padding: 1rem;
  cursor: pointer;
}
.option:hover {
  background-color: #2d213f;
}
.option.correct {
  background-color: #42b983;
}
.option.wrong {
  color: #f80008;
}
.option:last-of-type {
  margin-bottom: 0;
}
.option.disabled {
  opacity: 0.5;
}
.option input {
  background-color: #42b983;
}
button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
button:disabled:hover {
  color: #f80000;
}
</style>
