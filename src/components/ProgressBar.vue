<template>
  <div class="progress">
    <div
      class="progress-bar t-black"
      role="progressbar"
      aria-valuenow="0"
      aria-valuemin="0"
      aria-valuemax="100"
      :style="{ width: (current / total) * 100 + '%' }"
    >
      {{ current }} / {{ total }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    current: Number,
    total: Number,
  },
};
</script>

<style scoped></style>
