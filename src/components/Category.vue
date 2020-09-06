<template>
  <div class="row">
    <div class="col-12">
      <div class="card p-3 m-5">
        <form>
          <div class="form-group">
            <label for="category">Choose Category</label>
            <select
              name="category"
              id="category"
              class="form-control"
              v-model="selectedCategory"
            >
              <option
                v-for="category in categories"
                :key="category.id"
                :value="category.id"
              >
                {{ category.name }}
              </option>
            </select>
          </div>
          <button class="btn btn-success" @click.prevent="beginQuiz">
            Begin Quiz
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedCategory: 9,
      categories: [
        { id: 9, name: "General Knowledge" },
        { id: 10, name: "Entertainment: Books" },
        { id: 15, name: "Entertainment: Video Games" },
        { id: 17, name: "Science & Nature" },
        { id: 18, name: "Science: Computers" },
        { id: 19, name: "Science: Mathematics" },
        { id: 21, name: "Sports" },
        { id: 22, name: "Geography" },
        { id: 27, name: "Animals" },
        { id: 28, name: "Vehicles" },
      ],
      quiz: null,
    };
  },
  methods: {
    beginQuiz() {
      let result = {};
      result["category"] = this.selectedCategory;
      console.log("data", this.$data);
      this.$emit("categorySelected", result);
    },
  },
};
</script>

<style scoped></style>
