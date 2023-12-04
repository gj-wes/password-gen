<script setup>
defineProps({
  rank: String
})
</script>

<template>
  <div class="container">
    <label>
      Strength
    </label>

    <div class="indicator">
      <div class="text">
        {{ rank }}
      </div>

      <div class="indicator-lines">
        <template v-if="rank === 'too weak!'">
          <div class="weakest"></div>
          <div></div>
          <div></div>
          <div></div>
        </template>
        <template v-if="rank === 'weak'">
          <div class="weak"></div>
          <div class="weak"></div>
          <div></div>
          <div></div>
        </template>
        <template v-if="rank === 'medium'">
          <div class="medium"></div>
          <div class="medium"></div>
          <div class="medium"></div>
          <div></div>
        </template>
        <template v-if="rank === 'strong'">
          <div class="strong"></div>
          <div class="strong"></div>
          <div class="strong"></div>
          <div class="strong"></div>
        </template>
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

  & div:not(:is(.weakest, .weak, .medium, .strong)) {
    border: 2px solid var(--clr-almost-white)
  }
}

.weakest {
  border-color: var(--clr-accent-red);
  background-color: var(--clr-accent-red);
}
.weak {
  border-color: var(--clr-accent-orange);
  background-color: var(--clr-accent-orange);
}
.medium {
  border-color: var(--clr-accent-yellow);
  background-color: var(--clr-accent-yellow);
}
.strong {
  border-color: var(--clr-accent-primary);
  background-color: var(--clr-accent-primary);
}
</style>