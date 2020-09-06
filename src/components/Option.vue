<template>
  <button class="btn btn-info m-3 btn-block" @click="optionSelected">
    {{ option }}
  </button>
</template>

<script>
export default {
  props: {
    option: {
      type: String,
      default: "",
    },
    index: {
      type: Number,
      default: -1,
    },
  },
  directives: {
    "shadow-hover": {
      bind(el, binding) {
        let value = binding.value;
        el.addEventListener("mouseenter", () => {
          el.classList.add(value);
        });
        el.addEventListener("mouseleave", () => {
          el.classList.remove(value);
        });
      },
      unbind(el) {
        el.removeEventListener("mouseenter");
        el.removeEventListener("mouseleave");
      },
    },
  },
  methods: {
    optionSelected() {
      this.$emit("optionSelected", this.index);
    },
  },
};
</script>

<style scoped>
.option {
  cursor: pointer;
}
</style>
