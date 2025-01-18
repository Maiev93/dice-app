<template>
  <div class="result-view">
    <h3 class="result-view__header">
      Результат броска: {{ sumDices }} + {{ props.sumStats }} ({{ sumDices + props.sumStats }})
    </h3>
    <div class="result-view__content">
      <result-item v-for="res in props.result" :key="res.id" :name="res.name" :value="res.value" />
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

import ResultItem from './ResultItem.vue'

const props = defineProps({
  sumStats: {
    type: Number,
    default: 0,
  },
  result: {
    type: Array,
    required: true,
  },
})

const sumDices = computed(() => {
  let sum = 0
  props.result.forEach((el) => {
    sum += el.value
  })

  return sum
})
</script>

<style lang="scss" scoped>
.result-view {
  display: flex;
  flex-direction: column;
  align-items: center;

  &__content {
    display: flex;
    flex-wrap: wrap;
    gap: 5px;
  }
}
</style>
