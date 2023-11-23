<script setup>
defineProps({
  settings: Object
})
</script>

<template>
  <div class="container">
    <label>
      Strength
    </label>

    <div class="indicator">
      <div class="text">
        medium
      </div>

      <div class="indicator-lines">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
    </div>

  </div>
</template>

<style scoped>
.container {
  background-color: var(--clr-v-dark-grey);
  padding: 1.25rem 2rem;

  display: flex;
  justify-content: space-between;
  align-items: center;

  text-transform: uppercase;

  & label {
    color: var(--clr-grey);
  }
}

.indicator {
  display: flex;

  & .text {
    color: var(--clr-almost-white);
    font-size: var(--fs-m);

    margin-inline-end: 1rem;
  }
}

.indicator-lines {
  display: grid;
  grid-template-columns: repeat(4, 10px);
  gap: .5rem;

  & div {
    border: 2px solid var(--clr-almost-white)
  }
}
</style>