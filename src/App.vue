<template>
  <div id="app" class="relative" :class="[showModal === true ? 'bg-gray-700' : '']">
    <BoardGame />
    <Rules />
  </div>
</template>

<script>
import Rules from "./components/Rules.vue"
import BoardGame from "./components/BoardGame.vue"

export default {
  name: 'App',
  components: {
    Rules,
    BoardGame
  }
}

</script>

<style>
#app {
  font-family: 'Barlow Semi Condensed', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  padding: 5% 5% 1% 5%;
}

body {
  background-color: #1f3756;
  margin: 0;
  box-sizing: border-box;
}


</style>
