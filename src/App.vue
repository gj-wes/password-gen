<script setup>
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

  --fs-l: 2rem;
  --fs-m: 1.5rem;
  --fs-base: 1.125rem;

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
  margin:0 0 2rem 0;
  font-size: var(--fs-m);
  color: var(--clr-grey);
  text-align: center;
}

.checkbox-group > * + * {
  margin-block-start: 1.125rem;
}

.output,
.settings {
  padding: 2rem;
  background-color: var(--clr-dark-grey);

  & > * + * {
    margin-block-start: 2rem;
  }
}
.output {
  margin-block-end: 1.5rem;
}
</style>
