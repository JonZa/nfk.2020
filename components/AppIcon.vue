<template>
  <svg
    :height="height"
    :width="width"
    :fill="fill"
    xmlns="http://www.w3.org/2000/svg"
    viewBox="0 0 100 100"
  >
    <path
      fill="currentColor"
      d="M35.208 62.802c2.226-2.043 13.542-12.554 19.86-18.425-1.374-4.538-.181-9.659 3.53-13.101 3.696-3.43 8.873-4.248 13.289-2.563l-10.039 9.323 1.446 6.35 6.223 1.92 10.045-9.323c1.356 4.528.153 9.63-3.543 13.063-3.708 3.439-8.899 4.25-13.32 2.548A23485.7 23485.7 0 0142.84 71.026zM25.031 12.656c-13.55 0-22.5 8.337-22.5 20.844 0 7.333 3.559 15.525 11.719 23l35.125 32.625L84.469 56.5c8.16-7.474 11.719-15.667 11.719-23 0-12.507-8.944-20.844-22.5-20.844-12.628 0-16.92 5.47-24.313 13.375-7.391-7.906-11.717-13.375-24.344-13.375z"
    />
  </svg>
</template>

<script>
export default {
  props: {
    height: {
      type: Number,
      default: 40,
    },
    width: {
      type: Number,
      default: 40,
    },
    fill: {
      type: String,
      default: "#fff",
    },
  },
};
</script>

<style lang="scss" scoped>
svg {
  vertical-align: middle;
  margin-right: 10px;
}
</style>
