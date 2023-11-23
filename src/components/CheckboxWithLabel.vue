<script setup>
defineProps({
  labelText: String,
  modelValue: Boolean
})
defineEmits(['update:modelValue'])
</script>

<template>
  <label class="check-group">
    <input 
      type="checkbox" 
      :checked="modelValue" 
      @click="$emit('update:modelValue', $event.target.checked)"
    >
    {{ labelText }}
  </label>
</template>

<style scoped>
.check-group {
  color: var(--clr-almost-white);
  font-size: var(--fs-m);
  text-transform: capitalize;
  cursor: pointer;
  display: grid;
  grid-template-columns: 1.125rem auto;
  gap: 1.5rem;
}

input[type="checkbox"] {
  -webkit-appearance: none;
  appearance: none;
  background-color: inherit;
  margin: 0;
  width: 1.5rem;
  height: 1.5rem;
  border: 0.15em solid var(--clr-almost-white);
  display: grid;
  place-content: center;
  cursor: pointer;

  &:hover {
    border-color: var(--clr-accent-primary);
  }
}

input[type="checkbox"]::before {
  content: "";
  width: 1.5rem;
  height: 1.5rem;
  transform: scale(0);
  transition: 120ms transform ease-in-out;
  background-color: var(--clr-accent-primary);
  background-image: url('/icon-check.svg');
  background-position: center;
  background-size: 75%;
  background-repeat: no-repeat;
}
input[type="checkbox"]:checked::before {
  transform: scale(1);
}

</style>