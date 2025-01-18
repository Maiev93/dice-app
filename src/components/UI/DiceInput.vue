<template>
  <div class="dice-input">
    <label class="dice-input__label"
      >{{ props.label }}
      <input class="dice-input__input" type="text" v-model="model" />
    </label>
  </div>
</template>

<script setup>
const props = defineProps({
  label: {
    type: String,
    default: '',
  },
})

const model = defineModel()
</script>

<style lang="scss" scoped>
.dice-input {
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
      border: none;
      outline: 1px solid #87cefa;
    }
  }
}
</style>
