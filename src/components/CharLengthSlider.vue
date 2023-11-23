<script setup>
import { ref } from 'vue'
const length = ref(10)

defineProps({
  modelValue: Number
})
defineEmits(['update:modelValue'])
</script>

<template>
  <div class="label-group">
    <label for="char">Character length</label>
    <span class="current-length">{{ length }}</span>
  </div>
  <input type="range" id="char" min="1" max="20" v-model="length" @change="$emit('update:modelValue', +length)">
</template>

<style scoped>
.label-group {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-block-end: 1rem;
}
label {
  color: var(--clr-almost-white);
  font-size: var(--fs-m);
  text-transform: capitalize;
}
.current-length {
  color: var(--clr-accent-primary);
  font-size: var(--fs-l);
}
input[type="range"] {
  width: 100%;
  background-color: inherit;
  border: none;
  accent-color: var(--clr-accent-primary);
  cursor: pointer;

  /* &::-webkit-slider-runnable-track,
  &::-moz-range-track {
    background-color: var(--clr-v-dark-grey);
    height: 8px;
    border-radius: 0;
  }

  &::-webkit-slider-thumb,
  &::-moz-range-thumb {
    width: 28px;
    height: 28px;
    border-radius: 50%;
    background-color: var(--clr-almost-white);
    cursor: pointer;
  } */
}
</style>