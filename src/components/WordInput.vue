<template>

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
</template>

<script>
export default {
  name: "WordInput",
  data() {
    return {
      letterCount: 5,
      levels: [5, 6, 7, 8, 9, 10],
      correctLetters: [],
      misplacedLetters: [],
      wrongLetters: ""
    }
  },
  computed: {
    excludedLetters() {
      return this.wrongLetters.split("")
    }
  }
}
</script>

<style scoped>

.letter-input {
  width: 50px;
  height: 50px;
  text-align: center;
  font-size: 24px;
  margin: 5px;
  color: #fff;
  text-transform: uppercase;
}

.multiple {
  width: 100%;
}

.correct {
  background-color: green;
}

.misplaced {
  background-color: orange;
}

.wrong {
  background-color: gray;
}

</style>