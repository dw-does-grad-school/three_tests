// components/TicTacToe.vue
<template>
    <router-link
    to="/"
    class="fixed top-4 left-4 bg-[#ff5370] text-white font-bold py-2 px-4 rounded hover:bg-[#ff7a80] transition"
  >
    Return Home
  </router-link>
  <div class="flex flex-col items-center justify-center h-screen bg-[#1c1c1c] text-[#b5a642]">
    <h1 class="text-4xl font-bold mb-4">Tic Tac Toe - Breaking Bad Edition</h1>
    
    <div class="grid grid-cols-3 gap-2 w-64">
      <button v-for="(cell, index) in board" :key="index" @click="makeMove(index)"
        class="w-20 h-20 text-3xl font-bold flex items-center justify-center bg-[#2d2d2d] border border-[#b5a642] hover:bg-[#3d3d3d]">
        {{ cell }}
      </button>
    </div>
    
    <p v-if="winner" class="mt-4 text-2xl">{{ winner }} wins!</p>
    <p v-if="winner" class="text-lg cursor-pointer underline" @click="resetGame">Play Again</p>
    
    <div class="mt-6">
      <p>Player Wins: {{ playerWins }}</p>
      <p>Computer Wins: {{ computerWins }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const board = ref(Array(9).fill(""));
const player = "X";
const computer = "O";
const winner = ref(null);
const playerWins = ref(parseInt(localStorage.getItem("playerWins")) || 0);
const computerWins = ref(parseInt(localStorage.getItem("computerWins")) || 0);

const checkWinner = () => {
  const winningCombinations = [
    [0, 1, 2], [3, 4, 5], [6, 7, 8],
    [0, 3, 6], [1, 4, 7], [2, 5, 8],
    [0, 4, 8], [2, 4, 6]
  ];
  
  for (let combo of winningCombinations) {
    const [a, b, c] = combo;
    if (board.value[a] && board.value[a] === board.value[b] && board.value[a] === board.value[c]) {
      winner.value = board.value[a] === player ? "Player" : "Computer";
      if (winner.value === "Player") {
        playerWins.value++;
        localStorage.setItem("playerWins", playerWins.value);
      } else {
        computerWins.value++;
        localStorage.setItem("computerWins", computerWins.value);
      }
      return;
    }
  }
};

const makeMove = (index) => {
  if (board.value[index] || winner.value) return;
  board.value[index] = player;
  checkWinner();
  if (!winner.value) {
    setTimeout(computerMove, 500);
  }
};

const computerMove = () => {
  let emptyCells = board.value.map((cell, i) => (cell === "" ? i : null)).filter(i => i !== null);
  if (emptyCells.length === 0) return;
  let randomIndex = emptyCells[Math.floor(Math.random() * emptyCells.length)];
  board.value[randomIndex] = computer;
  checkWinner();
};

const resetGame = () => {
  board.value = Array(9).fill("");
  winner.value = null;
};
</script>