<template>
  <header>
    <h1 class="dice-app__header">Добро пожаловать в Dice App</h1>
  </header>

  <main class="dice-app__content">
    <div class="dice-app__dices-wrapper">
      <dices-view @change-dices="changeDices" />
      <dice-button class="dice-app__button" text="Бросок" @click="rollDices" />
      <result-view v-if="result.length" :sum-stats="sumStats" :result="result" />
    </div>

    <stats-view @change-stats="changeStats" />
  </main>

  <div class="dice-app__result" v-if="resultOld.length">
    <h2 class="dice-app__result-h">Прошлые броски</h2>
    <div class="dice-app__result-wrapper">
      <result-view
        class="dice-app__result-item"
        v-for="(res, index) in resultOld"
        :key="index"
        :sum-stats="res[0].mod"
        :result="res"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

import DicesView from './components/DicesView.vue'
import StatsView from './components/StatsView.vue'
import ResultView from './components/ResultView.vue'
import DiceButton from './components/UI/DiceButton.vue'

const dices = ref([])
const stats = ref([])
const result = ref([])
const resultOld = ref([])

const sumStats = computed(() => {
  let sum = 0

  stats.value.forEach((stat) => {
    if (stat.isCheck) {
      sum += stat.value
    }
  })

  return sum
})

onMounted(() => {
  getResultFromStorage()
})

function changeDices(value) {
  dices.value = value
}

function changeStats(value) {
  stats.value = value
}

function rollDices() {
  result.value = []

  dices.value.forEach((dice) => {
    if (dice.value > 0) {
      for (let index = 0; index < dice.value; index++) {
        const valueRandom = getRandomInt(1, dice.number)
        result.value.push({
          id: Date.now() + Math.random(),
          value: valueRandom,
          name: dice.name,
          number: dice.number,
          mod: sumStats.value,
        })
      }
    }
  })

  getResultFromStorage()
  setResultInStorage()
}

function getRandomInt(min, max) {
  min = Math.ceil(min)
  max = Math.floor(max)
  return Math.floor(Math.random() * (max - min + 1)) + min
}

function setResultInStorage() {
  if (!result.value.length) {
    return
  }

  try {
    const resultStorage = JSON.parse(localStorage.getItem('result'))
    if (resultStorage) {
      if (resultStorage.length > 10) {
        resultStorage.shift()
      }

      resultStorage.push(result.value)

      localStorage.setItem('result', JSON.stringify(resultStorage))
    } else {
      localStorage.setItem('result', JSON.stringify([result.value]))
    }
  } catch (error) {
    console.log(error)
  }
}

function getResultFromStorage() {
  try {
    if (JSON.parse(localStorage.getItem('result'))) {
      resultOld.value = JSON.parse(localStorage.getItem('result'))
    }
  } catch (error) {
    console.log(error)
  }
}
</script>

<style lang="scss" scoped>
.dice-app {
  &__header {
    text-align: center;
    font-weight: 600;
    background: -webkit-linear-gradient(45deg, #09009f, #00ff95 80%);
    background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  &__content {
    display: grid;
  }

  &__dices-wrapper {
    width: 320px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    justify-self: center;
  }

  &__button {
    width: 140px;
  }

  &__result-h {
    text-align: center;
    font-weight: 500;
    background: -webkit-linear-gradient(45deg, #09009f, #00ff95 80%);
    background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  &__result-wrapper {
    display: flex;
    flex-direction: column-reverse;
  }

  &__result-item {
    border-bottom: 1px solid var(--color-border);

    &:first-child {
      border: none;
    }
  }
}

@media (min-width: 768px) {
  .dice-app {
    &__content {
      grid-template-columns: 1fr 1fr;
    }
  }
}
</style>
