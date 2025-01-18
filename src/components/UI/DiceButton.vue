<template>
  <div class="dice-button">
    <button class="dice-button__button">
      {{ props.text }}
    </button>
  </div>
</template>

<script setup>
const props = defineProps({
  text: {
    type: String,
    default: '',
  },
})
</script>

<style lang="scss" scoped>
.dice-button {
  &__button {
    width: 100%;
    height: 40px;
    font-size: 16px;
    font-weight: 600;
    color: var(--color-text);
    background: rgb(135, 206, 250);
    background: linear-gradient(120deg, rgba(135, 206, 250, 1) 25%, rgba(72, 176, 44, 1) 100%);
    border-radius: 5px;
    border: none;
    cursor: pointer;

    &:hover {
      color: black;
      box-shadow: 0px 0px 16px 1px rgba(34, 60, 80, 0.2);
    }
  }
}
</style>
