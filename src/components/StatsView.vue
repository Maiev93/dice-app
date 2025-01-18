<template>
  <div class="stats">
    <h2 class="stats__header">Статы</h2>
    <div class="stats__content">
      <div class="stats__row" v-for="stat in stats" :key="stat.id">
        <dice-input v-model="stat.name" @input="changeValue(stat)" label="Название" />
        <dice-input-number v-model="stat.value" :name="stat.name" label="Значение" />
        <dice-checkbox v-model="stat.isCheck" :name="stat.name" label="Учесть" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref, watch } from 'vue'

import DiceInput from './UI/DiceInput.vue'
import DiceInputNumber from './UI/DiceInputNumber.vue'
import DiceCheckbox from './UI/DiceCheckbox.vue'

const $emits = defineEmits(['changeStats'])

const stats = ref([
  {
    id: 0,
    name: '',
    value: 0,
    isCheck: false,
  },
  {
    id: 1,
    name: '',
    value: 0,
    isCheck: false,
  },
  {
    id: 2,
    name: '',
    value: 0,
    isCheck: false,
  },
  {
    id: 3,
    name: '',
    value: 0,
    isCheck: false,
  },
  {
    id: 4,
    name: '',
    value: 0,
    isCheck: false,
  },
  {
    id: 5,
    name: '',
    value: 0,
    isCheck: false,
  },
  {
    id: 6,
    name: '',
    value: 0,
    isCheck: false,
  },
  {
    id: 7,
    name: '',
    value: 0,
    isCheck: false,
  },
  {
    id: 8,
    name: '',
    value: 0,
    isCheck: false,
  },
  {
    id: 9,
    name: '',
    value: 0,
    isCheck: false,
  },
])

onMounted(() => {
  try {
    if (JSON.parse(localStorage.getItem('stats'))) {
      stats.value = JSON.parse(localStorage.getItem('stats'))
    }
  } catch (error) {
    console.log(error)
  }
})

watch(
  () => stats,
  (newValue) => {
    $emits('changeStats', newValue.value)
    if (newValue) {
      localStorage.setItem('stats', JSON.stringify(stats.value))
    }
  },
  { deep: true },
)

function changeValue(stat) {
  if (!stat.name) {
    stat.isCheck = false
  }
}
</script>

<style lang="scss" scoped>
.stats {
  width: 320px;
  justify-self: center;

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
    display: flex;
    align-items: flex-end;
    gap: 5px;
  }
}
</style>
