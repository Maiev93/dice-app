<template>
  <div class="result">
    <span class="result__header">
      {{ props.name }}
    </span>
    <span class="result__value">
      {{ props.value }}
    </span>
  </div>
</template>

<script setup>
const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  value: {
    type: Number,
    required: true,
  },
})
</script>

<style lang="scss" scoped>
.result {
  display: grid;

  &__value {
    font-size: 18px;
    font-weight: 500;
  }
}
</style>
