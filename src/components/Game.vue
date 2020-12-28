<template>
  <div class="game">
    <div class="game-area">
      <div class="game-title">
        <h1>Tic Tac Toe</h1>
      </div>
      <Board :squares="squares" :winner="winner" @click="click" />
      <div class="game-info">
        <span v-if="stepNumber === 0"
          >It's your turn, {{ currentPlayer }}!</span
        >
        <span v-else-if="!!winner">
          The Winner is: {{ currentPlayer }}
          <button @click="restart"></button>
        </span>
        <span v-else-if="stepNumber === 9">
          It's a Draw!
          <button @click="restart">Play Again</button>
        </span>
        <span v-else>It's your turn, {{ currentPlayer }}!</span>
      </div>
    </div>
  </div>
</template>

<script>
import Board from './Board.vue';

export default {
  name: 'Game',
  components: { Board },
  data() {
    return {
      squares: Array(9).fill(null),
      stepNumber: 0,
      currentPlayer: 'X',
      winner: null,
    };
  },
  methods: {
    hasWinner() {
      if (this.winner) return true;

      const squares = this.squares;
      const matches = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];

      for (let i = 0; i < matches.length; i++) {
        const [a, b, c] = matches[i];
        if (
          squares[a] &&
          squares[a] === squares[b] &&
          squares[a] === squares[c]
        ) {
          this.winner = [a, b, c];
          return true;
        }
      }

      return false;
    },

    restart() {
      this.squares = Array(9).fill(null);
      this.stepNumber = 0;
      this.currentPlayer = 'X';
      this.winner = null;
    },

    click(i) {
      if (this.squares[i] || this.winner) return;
      this.$set(this.squares, i, this.currentPlayer);
      if (!this.hasWinner()) {
        this.stepNumber++;
        this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
      }
    },
  },
};
</script>

<style scoped>
.game {
  background-color: rgb(188, 237, 188);
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.game-area {
  display: flex;
  flex-flow: column;
}

.game-title {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 0 3vmin;
}

.game-title img {
  margin: 0 12px 0 -20px;
  width: 40px;
}

.game-title h1 {
  margin: 0;
  font-size: 2.25em;
  color: rgb(94, 186, 94);
  text-shadow: -1px -1px 1px #000b;
}

.game-info {
  margin: 3vmin 0 0;
  padding: 1rem 0.5rem;
  font-size: 1.25em;
  text-align: center;
  box-shadow: 2.5px 5px 25px #0001, 0 1px 6px #0004;
  text-shadow: 0 0 1px #fff, 0 2px 5px #fff5;
  border-radius: 0.5rem;
  background: #fff6;
  color: #111;
}

.game-info p {
  margin: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

.game-info .X {
  color: #ff5722;
}

.game-info .O {
  color: #ffeb3b;
}

.game-info button {
  text-transform: uppercase;
  font-weight: 600;
  font-size: 0.75em;
  padding: 0.5rem 1rem;
  margin: -0.5rem 0 -0.5rem 1rem;
  border: 2px solid #fff;
  background: #fff5;
  text-shadow: 0 0 1px #fff, 0 2px 5px #fff5;
  color: #111;
  cursor: pointer;
  outline: none;
  transition: all 0.25s ease;
}

.game-info button:focus,
.game-info button:hover {
  background: rgba(80, 80, 80, 0.333);
}

.game-info button:active {
  background: #1119;
}
</style>
