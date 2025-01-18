<template>
  <div class="dices">
    <h2 class="dices__header">Дайсы</h2>
    <div class="dices__content">
      <div class="dices__row" v-for="dice in dices" :key="dice.id">
        <component class="dices__image" :is="morphs[dice.name]"></component>
        <span class="dices__name">{{ dice.name }}</span>
        <dice-input-number v-model="dice.value" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

import DiceInputNumber from './UI/DiceInputNumber.vue'

// Icons
import d4 from './icons/IconD4.vue'
import d6 from './icons/IconD6.vue'
import d8 from './icons/IconD8.vue'
import d10 from './icons/IconD10.vue'
import d12 from './icons/IconD12.vue'
import d20 from './icons/IconD20.vue'
import d100 from './icons/IconD100.vue'

const $emits = defineEmits(['changeDices'])

const morphs = {
  d4,
  d6,
  d8,
  d10,
  d12,
  d20,
  d100,
}

const dices = ref([
  {
    id: 0,
    value: 0,
    name: 'd4',
    number: 4,
  },
  {
    id: 1,
    value: 0,
    name: 'd6',
    number: 6,
  },
  {
    id: 2,
    value: 0,
    name: 'd8',
    number: 8,
  },
  {
    id: 3,
    value: 0,
    name: 'd10',
    number: 10,
  },
  {
    id: 4,
    value: 0,
    name: 'd12',
    number: 12,
  },
  {
    id: 5,
    value: 0,
    name: 'd20',
    number: 20,
  },
  {
    id: 6,
    value: 0,
    name: 'd100',
    number: 100,
  },
])

watch(
  () => dices,
  (newValue) => {
    $emits('changeDices', newValue.value)
  },
  { deep: true },
)
</script>

<style lang="scss" scoped>
.dices {
  &__header {
    text-align: center;
    font-weight: 500;
    background: -webkit-linear-gradient(45deg, #09009f, #00ff95 80%);
    background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  &__content {
    display: grid;
    justify-content: center;
    gap: 5px;
  }

  &__row {
    display: grid;
    grid-template-columns: 30px 30px auto;
    align-items: center;
    gap: 5px;
  }

  &__image {
    width: 30px;
    height: 30px;
    color: rgb(135, 206, 250);
  }
}
</style>
