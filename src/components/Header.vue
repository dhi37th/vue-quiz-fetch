<template>
  <div>
    <div class="row mt-5 d-flex justify-content-center border-bottom">
      <h2>{{ categoryName }}</h2>
    </div>
    <div class="row my-3">
      <div class="col-12 p-2">
        <q-progress
          :current="questionAnswered"
          :total="totalQuestions"
        ></q-progress>
      </div>
    </div>
  </div>
</template>

<script>
import ProgressBar from "./ProgressBar.vue";
export default {
  components: {
    qProgress: ProgressBar,
  },
  props: {
    questionAnswered: {
      type: Number,
      default: 0,
    },
    totalQuestions: {
      type: Number,
      default: 10,
    },
    categoryName: {
      type: String,
      default: "The Super Quiz",
    },
  },
};
</script>

<style scoped></style>
