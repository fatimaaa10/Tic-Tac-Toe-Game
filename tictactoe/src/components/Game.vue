<template>
    <div class="board">
      <div v-for="(cell, index) in board" :key="index" class="cell" @click="makeMove(index)">
        {{ cell }}
      </div>
      <div v-if="winner" class="winner">
        {{ winner }} wins!
      </div>
      <div v-else-if="isDraw" class="winner">
        Draw!
      </div>
      <button @click="resetGame">Reset Game</button>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const board = ref(Array(9).fill(null));
  const currentPlayer = ref('X');
  const winner = ref(null);
  const isDraw = ref(false);
  
  const winningCombinations = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
  ];
  
  const makeMove = (index) => {
    if (!board.value[index] && !winner.value) {
      board.value[index] = currentPlayer.value;
      if (checkWinner()) {
        winner.value = currentPlayer.value;
      } else if (board.value.every(cell => cell !== null)) {
        isDraw.value = true;
      } else {
        currentPlayer.value = currentPlayer.value === 'X' ? 'O' : 'X';
      }
    }
  };
  
  const checkWinner = () => {
    return winningCombinations.some(combination => {
      const [a, b, c] = combination;
      return board.value[a] && board.value[a] === board.value[b] && board.value[a] === board.value[c];
    });
  };
  
  const resetGame = () => {
    board.value = Array(9).fill(null);
    currentPlayer.value = 'X';
    winner.value = null;
    isDraw.value = false;
  };
  </script>
  
  <style scoped>
  .board {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
    justify-content: center;
    margin-top: 40px;
    padding: 20px;
    background-color: #ffecd2; 
    border: 1px solid rgb(231, 78, 185); 
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    transform: scale(1.1);
  }

  .cell {
    width: 100%;
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2em;
    border: 1px solid rgb(231, 78, 185); 
    cursor: pointer;
    background-color: #fff2cc; 
    transition: background-color 0.2s ease;
    transform: scale(1.05);
  }

  .cell:hover {
    background-color: #ffe0b2; 
    transform: scale(1.1);
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  }

  .winner {
    margin-top: 20px;
    font-size: 1.5em;
    font-weight: bold;
    color: #e3338b; 
    text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.1);
  }

  button {
    margin-top: 20px;
    padding: 10px 20px;
    font-size: 1em;
    border: none;
    border-radius: 5px;
    background-color: rgb(231, 78, 185); 
    color: #fff;
    cursor: pointer;
    display: block;
    margin: 20px auto;
    transform: scale(1.05);
  }

  button:hover {
    background-color: #ff99cc; 
    transform: scale(1.1);
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  }
  
</style>