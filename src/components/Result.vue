<template>
  <div
    :class="{ correct: isAnswerCorrect, incorrect: !isAnswerCorrect }"
    class="border p-4"
  >
    <div class="row my-5 d-flex justify-content-center border-bottom">
      <h2 v-if="isAnswerCorrect">That's correct</h2>
      <h2 v-else>That's incorrect</h2>
    </div>
    <div class="row">
      <div v-if="!quizEnd" class="col-12 d-flex justify-content-center">
        <button class="btn btn-primary" @click="nextQuestion">
          Next Question
        </button>
      </div>
      <div v-else class="col-12">
        <div class="row d-flex justify-content-center">
          <p>You answered {{ totalCorrect }} correct.</p>
        </div>
        <div class="row d-flex justify-content-center">
          <button class="btn btn-success" @click="newQuiz">
            New Quiz?
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    isAnswerCorrect: {
      type: Boolean,
      default: false,
    },
    quizEnd: {
      type: Boolean,
      default: false,
    },
    totalCorrect: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    nextQuestion() {
      this.$emit("nextQuestion");
    },
    newQuiz() {
      this.$emit("startNewQuiz");
    },
  },
};
</script>

<style scoped>
.correct {
  background-color: lightgreen;
}

.incorrect {
  background-color: lightcoral;
}
</style>
