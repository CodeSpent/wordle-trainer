<template>

  <h1 class="header">Wordle Trainer</h1>

  <div style="display: flex; flex-direction: column;">
    <h2>Select Letter Count</h2>

    <select v-model="letterCount" style="width: 100px; margin: auto;">
      <option v-for="i in levels" :value="i" :key="i">{{ i }}</option>
    </select>
  </div>

  <div style="display: flex; flex-direction: column;">
    <h2>Correct Letters</h2>

    <div style="display: flex; margin: auto;">
      <input class="letter-input correct" v-for="(i, n) in letterCount" :key="i" v-model="correctLetters[n]"
             maxlength="1">
    </div>
  </div>

  <div style="display: flex; flex-direction: column;">
    <h2>Misplaced Letters</h2>

    <div style="display: flex; margin: auto;">
      <input class="letter-input misplaced" v-for="(i, n) in letterCount" :key="i" v-model="misplacedLetters[n]"
             maxlength="1">
    </div>
  </div>

  <div style="display: flex; flex-direction: column;">
    <h2>Excluded Letters</h2>

    <div style="display: flex; margin: auto;">
      <input class="letter-input multiple wrong" v-model="wrongLetters">
    </div>
  </div>

  <h2>Potential Words:</h2>
  <div style="display: flex;">
    <span v-for="word in potentialWords" :key="word">{{ word }}, </span>
  </div>

</template>

<script>
import {words} from '@/data/words';

export default {
  name: "WordInput",
  data() {
    return {
      letterCount: 5,
      levels: [5, 6, 7, 8, 9, 10],
      correctLetters: [],
      misplacedLetters: [],
      wrongLetters: "",
    }
  },
  computed: {
    excludedLetters() {
      return this.wrongLetters.split("")
    },
    potentialWords() {
      return this.fetchPotentialWords()
    }
  },
  watch: {
    correctLetters: {
      handler: function () {
        this.fetchPotentialWords()
      },
      deep: true
    }
  },
  methods: {
    fetchPotentialWords() {
      return words
          .filter(word =>
              // Verify word is correct length
              (word.length === this.letterCount) &&
              // Verify that letters are in the correct index in the word
              (this.correctLetters.every((letter, i) => !letter || word[i] === letter)) &&
              // Verify that misplaced letters are in the word, but not at current index
              (this.misplacedLetters.every((letter, i) => !letter || word.includes(letter.toLowerCase()) && word[i] !== letter)) &&
              // Verify that excluded letters are not in the word at all
              (this.excludedLetters.every(letter => !word.includes(letter.toLowerCase())))
          );
    }

  }
}
</script>

<style scoped>
.header {
  margin: auto;
  font-size: 48px;
  font-style: italic;
  border-style: solid;
  border-width: 0 0 4px 0;
  padding-bottom: 1px;
  width: fit-content;
  border-image: linear-gradient(45deg, #6aaa64, #c9b458) 1;
}

.letter-input {
  width: 50px;
  height: 60px;
  text-align: center;
  font-size: 24px;
  margin: 5px;
  color: #fff;
  text-transform: uppercase;
  border: none;
  border-radius: 10px;
}

.multiple {
  width: 100%;
}

.correct {
  background-color: #6aaa64;
}

.misplaced {
  background-color: #c9b458;
}

.wrong {
  background-color: #787c7e;
}
</style>