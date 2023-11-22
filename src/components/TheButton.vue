<script setup>
import IconArrowRight from './IconArrowRight.vue'
</script>

<template>
  <button>
    <slot /> <IconArrowRight />
  </button>
</template>

<style scoped>
button {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1.5rem;
  width: 100%;
  padding-block: 1.25rem;
  background-color: var(--clr-accent-primary);
  border: 1px solid var(--clr-accent-primary);

  font-family: inherit;
  color: var(--clr-v-dark-grey);
  font-size: var(--fs-base);
  text-transform: uppercase;

  transition: background-color .1s linear, color .1s linear;

  &:hover {
    background-color: var(--clr-dark-grey);
    color: var(--clr-accent-primary);
  }
  &:hover :deep(path) {
    fill: var(--clr-accent-primary);
  }
}
</style>