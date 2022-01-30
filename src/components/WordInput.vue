<template>
  <div style="display: flex; flex-direction: column;">
    <h2>Correct Letters</h2>

    <div style="display: flex; margin: auto;">
      <input class="letter-input correct" v-for="i in letterCount" :key="i" maxlength="1">
    </div>
  </div>

  <div style="display: flex; flex-direction: column;">
    <h2>Misplaced Letters</h2>

    <div style="display: flex; margin: auto;">
      <input class="letter-input misplaced" v-for="i in letterCount" :key="i" maxlength="1">
    </div>
  </div>

  <div style="display: flex; flex-direction: column;">
    <h2>Excluded Letters</h2>

    <div style="display: flex; margin: auto;">
      <input class="letter-input multiple wrong">
    </div>
  </div>

  <h2>Potential Words:</h2>
</template>

<script>
export default {
  name: "WordInput",
  data() {
    return {
      letterCount: 5
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