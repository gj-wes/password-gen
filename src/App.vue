<script setup>
import IconCopy from './composables/IconCopy.vue';
import CharLengthSlider from './components/CharLengthSlider.vue';
import CheckboxWithLabel from './components/CheckboxWithLabel.vue';
import StrengthIndicator from './components/StrengthIndicator.vue';
import TheButton from './components/TheButton.vue';

import { ref, reactive } from 'vue';
import { useClipboard } from '@vueuse/core'

const settings = reactive({
  length: 10,
  uppercase: true,
  lowercase: true,
  numbers: false,
  symbols: false,
})

const passwordOutput = ref('')
const { copy } = useClipboard()

function randomInt (min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min
}

const strengthRank = ref("medium");

function generate() {
  const uppercase = ["A","B","C","D","E","F","G","H","I","J","K","L","M","N","O","P","Q","R","S","T","U","V","W","X","Y","Z"];
  const lowercase = ["a","b","c","d","e","f","g","h","i","j","k","l","m","n","o","p","q","r","s","t","u","v","w","x","y","z"];
  const numbers = ['0','1','2','3','4','5','6','7','8','9'];
  const symbols = ['+','-','/','*','<','>','~','(',')','[',']','!','@','£','#','$','%','&','?','.',',','|','^'];

  // Combined character arrays based on checked settings
  let selected = []
  let selectedCount = 0;

  // Could be a better way to do this?
  if (settings.uppercase) {
    selected = [...selected, ...uppercase]
    selectedCount++
  }
  if (settings.lowercase) {
    selected = [...selected, ...lowercase]
    selectedCount++
  }
  if (settings.numbers) {
    selected = [...selected, ...numbers]
    selectedCount++
  }
  if (settings.symbols) {
    selected = [...selected, ...symbols]
    selectedCount++
  }

  // Shuffle the combined array
  const selection = selected.map((a) => ({ sort: Math.random(), value: a }))
          .sort((a, b) => a.sort - b.sort)
          .map((a) => a.value);

  let result = [];

  // select random characters from shuffled array
  for (let i = 0; i < settings.length; i++) {
    const ind = randomInt(0, selection.length)
    result.push(selection[ind])
  }

  passwordOutput.value = result.join('')

  // Strength ranking
  const rank = Math.floor(selectedCount * settings.length)
  if (rank >= 70) {
    strengthRank.value = "strong"
  } else if (rank >= 45 && rank < 70) {
    strengthRank.value = "medium"
  } else if (rank >= 20 && rank < 45) {
    strengthRank.value = "weak"
  } else {
    strengthRank.value = "too weak!"
  }

  selected = []
  selectedCount = 0
  result = []
  return
}
</script>

<template>
  <main>
    <h1>
      Password Generator
    </h1>

    <div class="output">
      <textarea rows="1" :value="passwordOutput" class="password" placeholder="P4$5W0rD!" />

      <button class="copy" @click="copy(passwordOutput)" :disabled="passwordOutput.length === 0">
        <IconCopy />
      </button>
    </div>

    <div class="settings">
      <!-- Slider and length -->
      <CharLengthSlider v-model="settings.length" />

      <!-- checkbox & label x4 -->
      <div class="checkbox-group">
        <CheckboxWithLabel v-model="settings.uppercase" labelText="Include uppercase letters" />
        <CheckboxWithLabel v-model="settings.lowercase" labelText="Include lowercase letters" />
        <CheckboxWithLabel v-model="settings.numbers" labelText="Include numbers" />
        <CheckboxWithLabel v-model="settings.symbols" labelText="Include symbols" />
      </div>

      <!-- strength indicator -->
      <StrengthIndicator :rank="strengthRank" />
      
      <!-- generate button -->
      <TheButton @click="generate">generate</TheButton>
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

    &[disabled] {
      cursor: default;
    }
    &[disabled] :deep(path) {
      fill: var(--clr-grey);
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
