<template>
  <div id="app">
    <h1>Tic-Tac-Toe</h1>
    <Game />
  </div>
</template>

<script setup>
import Game from './components/Game.vue'
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: rgb(231, 78, 185);
  text-align: center;
  margin: auto;
}
</style>