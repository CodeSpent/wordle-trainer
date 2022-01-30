<template>
  <WordInput/>
</template>

<script>
import WordInput from "@/components/WordInput";

export default {
  name: 'App',
  components: {
    WordInput,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fff;
  margin-top: 60px;
}

html {
  background-color: rgb(32, 32, 32);
}
</style>
