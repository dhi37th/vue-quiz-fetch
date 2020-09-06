<template>
  <div class="container">
    <div class="row">
      <div class="col-12 d-fex justify-content-center">
        <q-category
          v-if="!isCategorySelected"
          @categorySelected="categorySelected"
        ></q-category>
        <q-question-grid
          v-else
          :category="categoryValue"
          @startNewQuiz="startNewQuiz"
        ></q-question-grid>
      </div>
    </div>
  </div>
</template>

<script>
import Category from "./components/Category.vue";
import QuestionGrid from "./components/QuestionGrid.vue";
export default {
  components: {
    qCategory: Category,
    qQuestionGrid: QuestionGrid,
  },
  data() {
    return {
      isCategorySelected: false,
      categoryValue: -1,
      questions: [],
    };
  },
  methods: {
    categorySelected(value) {
      this.isCategorySelected = true;
      this.categoryValue = value.category;
    },
    startNewQuiz() {
      this.isCategorySelected = false;
      this.questions = [];
      this.categoryValue = -1;
    },
  },
};
</script>

<style scoped></style>
