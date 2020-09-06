<template>
  <div>
    <div v-if="loading" class="row d-flex justify-content-center m-5">
      <div class="spinner-grow text-info" role="status">
        <span class="sr-only">Loading...</span>
      </div>
    </div>
    <div v-else>
      <q-header
        :totalQuestions="totalQuestions"
        :questionAnswered="currentIndex + 1"
        :categoryName="currentCategoryName"
      ></q-header>
      <transition
        name="r-trans"
        enter-active-class="animated fadeInLeft faster"
        leave-active-class="animated fadeOutRight faster"
        mode="out-in"
      >
        <q-question
          v-if="!currentAnswered"
          :question="currentQuestion"
          @questionAnswered="questionAnswered"
        ></q-question>
        <q-result
          v-else
          :isAnswerCorrect="isAnswerCorrect"
          :quizEnd="quizEnd"
          :totalCorrect="totalCorrect"
          @startNewQuiz="startNewQuiz"
          @nextQuestion="nextQuestion"
        ></q-result>
      </transition>
    </div>
  </div>
</template>

<script>
import Header from "./Header.vue";
import Question from "./Question.vue";
import Result from "./Result.vue";
export default {
  components: {
    qHeader: Header,
    qQuestion: Question,
    qResult: Result,
  },
  props: {
    category: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      questions: [],
      currentQuestion: null,
      currentOptions: [],
      currentIndex: 0,
      currentAnswered: false,
      currentCategoryName: "",
      isAnswerCorrect: false,
      totalQuestions: 10,
      totalCorrect: 0,
      loading: true,
      quizEnd: false,
    };
  },
  created() {
    let url =
      "https://opentdb.com/api.php?amount=" +
      this.totalQuestions +
      "&category=" +
      this.category;
    fetch(url)
      .then((response) => response.json())
      .then((data) => {
        this.questions = data.results;
        this.loading = false;
        this.setQuestion(this.currentIndex);
        this.totalQuestions = 10;
      });
  },
  methods: {
    setQuestion(index) {
      this.currentQuestion = this.questions[index];
      this.currentCategoryName = this.currentQuestion.category;
    },
    questionAnswered(value) {
      if (this.currentIndex == this.totalQuestions - 1) {
        this.quizEnd = true;
      }
      if (value) {
        this.totalCorrect++;
      }
      this.isAnswerCorrect = value;
      this.currentAnswered = true;
    },
    nextQuestion() {
      if (++this.currentIndex < this.totalQuestions) {
        this.currentAnswered = false;
        this.isAnswerCorrect = false;
        this.setQuestion(this.currentIndex);
      }
    },
    startNewQuiz() {
      this.$emit("startNewQuiz");
    },
  },
};
</script>

<style scoped></style>
