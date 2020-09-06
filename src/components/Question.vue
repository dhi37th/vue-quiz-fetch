<template>
  <div>
    <div class="card">
      <div class="card-header">
        <p>{{ question.question }}</p>
      </div>
      <div class="card-body">
        <div class="row">
          <q-option
            v-for="(option, index) in optionArray"
            :key="index"
            :index="index"
            :option="option"
            @optionSelected="optionSelected"
          ></q-option>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Option from "./Option.vue";
export default {
  components: {
    qOption: Option,
  },
  props: {
    question: {
      type: Object,
      default: null,
    },
  },
  data() {
    return {
      optionArray: [],
      correctIndex: -1,
    };
  },
  created() {
    let arr = this.shuffleArray([
      this.question.correct_answer,
      ...this.question.incorrect_answers,
    ]);
    this.correctIndex = arr.indexOf(this.question.correct_answer);
    this.optionArray = arr;
  },
  methods: {
    shuffleArray(arr) {
      for (var i = arr.length - 1; i > 0; i--) {
        var j = Math.floor(Math.random() * (i + 1));
        var temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
      }
      return arr;
    },
    optionSelected(value) {
      this.$emit("questionAnswered", value === this.correctIndex);
    },
  },
};
</script>

<style scoped></style>
