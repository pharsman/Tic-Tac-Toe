<template>
  <h1>Tic Toc Toe</h1>
  <h2>Players {{ player }}'s turn</h2>
  <button @click="resetGame">Reset</button>
  <section>
    <div v-for="(row,x) in board" :key="x">
      <div class="box" v-for="(cell,y) in row" :key="y" @click="makeMove(x,y)">
        <h1 class="turn">{{cell === 'X' ? 'X' : cell ==='O' ? 'O': ''}} </h1>
      </div>
    </div>
  </section>
  <h1 v-if="winner" class="won">Player {{ winner }} Won !</h1>
</template>

<script setup>
import { ref, computed } from 'vue';

const player = ref('X')

const board = ref([
  ['', '', ''],
  ['', '', ''],
  ['', '', ''],
])

const calculateWinner = (board) => {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (board[a] && board[a] === board[b] && board[a] === board[c]) {
      return board[a];
    }
  }
  return null;
}

const winner = computed(() => {
  return calculateWinner(board.value.flat())
})

const makeMove = (x, y) => {
  if (winner.value) {
    return
  }
  if (board.value[x][y] !== '') {
    return
  }
  board.value[x][y] = player.value
  player.value = player.value === 'X' ? 'O' : 'X'
}

const resetGame = () => {
  board.value = [
    ['', '', ''],
    ['', '', ''],
    ['', '', ''],
  ]
  player.value = 'X'
}

</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #383535;
}

h1 {
  color: #ffffff;
  text-align: center;
  font-size: 70px;
  margin-top: 2rem;
}

h2 {
  color: #ffffff;
  text-align: center;
  font-size: 40px;
  margin-top: 2rem;
}

.won {
  margin-left: 1200px;
  margin-top: -450px;
  color: #ff0000;
}

button {
  background-color: #eb16c7;
  color: #ffffff;
  padding: 10px 30px;
  font-size: 40px;
  border: none;
  border-radius: 30px;
  margin-top: 200px;
  margin-left: 200px;
  cursor: pointer;
}


section {
  margin: -200px auto;
  width: 600px;
  height: 600px;
  background-color: #21087a;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;

  .box {
    width: 200px;
    height: 200px;
    text-align: center;
    border: 2px solid red;
    cursor: pointer;

    .turn {
      color: #ffffff;
      margin-top: 35%;
      font-size: 50px;
    }
  }
}
</style>