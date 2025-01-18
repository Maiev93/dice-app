<template>
  <div class="dice-input-number">
    <label class="dice-input-number__label"
      >{{ props.label }}
      <input
        class="dice-input-number__input"
        type="number"
        :name="props.name"
        min="0"
        max="100"
        v-model="model"
        @input="checkValue"
      />
    </label>
  </div>
</template>

<script setup>
const props = defineProps({
  label: {
    type: String,
    default: '',
  },
  name: {
    type: String,
    default: '',
  },
})

const model = defineModel()

function checkValue(event) {
  if (event.target.value > 100) {
    model.value = 100
  }
}
</script>

<style lang="scss" scoped>
.dice-input-number {
  &__label {
    display: grid;
    font-size: 12px;
  }

  &__input {
    max-width: 100px;
    height: 30px;
    border: 1px solid var(--color-border);
    border-radius: 4px;

    &:focus {
      border-color: transparent;
      outline: 1px solid #87cefa;
    }
  }
}
</style>
