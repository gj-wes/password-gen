<script setup>
import IconCopy from './composables/IconCopy.vue';
import CharLengthSlider from './components/CharLengthSlider.vue';
import CheckboxWithLabel from './components/CheckboxWithLabel.vue';
import StrengthIndicator from './components/StrengthIndicator.vue';
import TheButton from './components/TheButton.vue';
</script>

<template>
  <main>
    <h1>
      Password Generator
    </h1>

    <div class="output">
      <textarea rows="1" class="password" placeholder="P4$5W0rD!" />

      <button class="copy">
        <IconCopy />
      </button>
    </div>

    <div class="settings">
      <!-- Slider and length -->
      <CharLengthSlider />

      <!-- checkbox & label x4 -->
      <div class="checkbox-group">
        <CheckboxWithLabel labelText="Include uppercase letters" />
        <CheckboxWithLabel labelText="Include lowercase letters" />
        <CheckboxWithLabel labelText="Include numbers" />
        <CheckboxWithLabel labelText="Include symbols" />
      </div>

      <!-- strength indicator -->
      <StrengthIndicator />
      
      <!-- generate button -->
      <TheButton>generate</TheButton>
    </div>
  </main>
</template>

<style scoped>
:global(*) {
  box-sizing: border-box;
}
:global(:root) {
  --clr-almost-white: #E6E5EA;
  --clr-grey: #817D92;
  --clr-dark-grey: #24232C;
  --clr-v-dark-grey: #18171F;

  --clr-accent-primary: #A4FFAF;
  --clr-accent-red: #F64A4A;
  --clr-accent-orange: #FB7C58;
  --clr-accent-yellow: #F8CD65;

  --fs-l: clamp(1.5rem, 1.324rem + 0.751vw, 2rem);
  --fs-m: clamp(1rem, 0.824rem + 0.751vw, 1.5rem);
  --fs-base: clamp(1rem, 0.956rem + 0.188vw, 1.125rem);

  --lh-base: 1.3
}

:global(body) {
  margin:0;
}

:global(#app) {
  margin: 0;
  background-color: var(--clr-v-dark-grey);
  font-family: 'JetBrains Mono', monospace;
  font-size: var(--fs-base);
  line-height: var(--lh-base);
}

main {
  --padding-inline: 1rem;

  min-height: 100vh;
  display: grid;
  place-content: center center;
  grid-template-columns: minmax(var(--padding-inline), 1fr) [content-start] min(100% - (var(--padding-inline) * 2), 540px) [content-end] minmax(var(--padding-inline), 1fr);
}

main > * {
  grid-column: content;
}

h1 {
  margin:0 0 clamp(1rem, 0.6479rem + 1.5023vw, 2rem) 0;
  font-size: var(--fs-m);
  color: var(--clr-grey);
  text-align: center;
}

.output {
  padding: 1.125rem clamp(1rem, 0.6479rem + 1.5023vw, 2rem);
  background-color: var(--clr-dark-grey);
  margin-block-end: 1.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;

  & .password {
    resize: none;
    border: none;
    background: none;
    flex-grow: 1;

    font-size: var(--fs-l);
    font-family: inherit;
    color: var(--clr-almost-white);
  }

  & .copy {
    border: none;
    background: none;
    cursor: pointer;

    &:hover :deep(path) {
      fill: var(--clr-almost-white)
    }
  }
}

.settings {
  padding: clamp(1rem, 0.6479rem + 1.5023vw, 2rem);;
  background-color: var(--clr-dark-grey);
  & > * + * {
    margin-block-start: clamp(1rem, 0.6479rem + 1.5023vw, 2rem);
  }
}
.checkbox-group > * + * {
  margin-block-start: 1.125rem;
}
</style>
