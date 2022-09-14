<template>
    <section>
        <div @click="put" class="box"></div>
        <div @click="put" class="box"></div>
        <div @click="put" class="box"></div>
        <div @click="put" class="box"></div>
        <div @click="put" class="box"></div>
        <div @click="put" class="box"></div>
        <div @click="put" class="box"></div>
        <div @click="put" class="box"></div>
        <div @click="put" class="box"></div>
    </section>
</template>

<script setup>
import { ref, computed } from 'vue';

const player = ref('X')

const board = ref([
    ['', '', ''],
    ['', '', ''],
    ['', '', ''],
])

const calculateWinner = (squares) => {
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
        if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
            return squares[a];
        }
    }
    return null;
}

const winner = computed(() => {
    calculateWinner(board.value.flat())
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

<style scoped lang="scss">
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

section {
    margin: 80px auto;
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

        h1 {
            color: #ffffff;
            margin-top: 35%;
            font-size: 50px;
        }
    }
}
</style>