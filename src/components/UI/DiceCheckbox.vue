<template>
  <div class="dice-checkbox">
    <span class="dice-checkbox__label">{{ props.label }}</span>
    <label class="dice-checkbox__name" :class="{ _disabled: !props.name }" :for="props.name">
      <icon-check v-if="model" />
    </label>
    <input v-show="false" type="checkbox" :name="props.name" :id="props.name" v-model="model" />
  </div>
</template>

<script setup>
import IconCheck from '../icons/IconCheck.vue'

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
</script>

<style lang="scss" scoped>
.dice-checkbox {
  display: grid;

  &__label {
    font-size: 12px;
  }

  &__name {
    display: inline-block;
    width: 30px;
    height: 30px;
    border-radius: 5px;
    border: 1px solid var(--color-border);
    background-color: var(--color-background);
  }

  ._disabled {
    cursor: not-allowed;
    background: var(--color-background-mute);
  }
}
</style>
