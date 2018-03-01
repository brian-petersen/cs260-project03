<template>
  <div>
    <div class="wrapper">
      <board :board="board" @click="boardClick" />
    </div>

    <div v-if="hasWinner" class="instructions">
      Player {{ winner }} won!
    </div>
    <div v-else-if="isDraw" class="instructions">
      Game ended as a draw.
    </div>
    <div v-else class="instructions">
      {{ currentTurn }}
    </div>

    <div v-if="isDraw || hasWinner">
      <button @click="playAgain">Play Again</button>
    </div>
  </div>
</template>

<script>
import Board from './Board';

const BOARD_SIZE = 3;

function initialState() {
  return {
    xTurn: true,
    moveCount: 0,
    board: [
      ['', '', ''],
      ['', '', ''],
      ['', '', '']
    ],
    isDraw: false,
    hasWinner: false,
    winner: null
  };
}

export default {
  data() {
    return initialState();
  },
  methods: {
    boardClick(row, col) {
      // valid move
      if (this.isDraw || this.hasWinner || this.board[row][col] !== '')
        return;

      const playerSymbol = this.xTurn ? 'X' : 'O';

      // update position
      const newRow = this.board[row];
      if (this.xTurn)
        newRow[col] = playerSymbol;
      else
        newRow[col] = playerSymbol;
      this.$set(this.board, row, newRow);

      // check winner
      if (this.moveWon(row, col, playerSymbol)) {
        this.hasWinner = true;
        this.winner = playerSymbol;
        return;
      }

      // check draw
      if (this.checkDraw()) {
        this.isDraw = true;
        return;
      }

      // change turn
      this.xTurn = !this.xTurn;
      this.moveCount++;
    },
    moveWon(row, col, player) {
      // check column
      for (let i = 0; i < BOARD_SIZE; i++) {
        if (this.board[i][col] !== player)
          break;

        if (i === BOARD_SIZE - 1)
          return true;
      }

      // check row
      for (let i = 0; i < BOARD_SIZE; i++) {
        if (this.board[row][i] !== player)
          break;

        if (i === BOARD_SIZE - 1)
          return true;
      }

      // check diagonal
      if (row === col) {
        for (let i = 0; i < BOARD_SIZE; i++) {
          if (this.board[i][i] !== player)
            break;

          if (i === BOARD_SIZE - 1)
            return true;
        }
      }

      // check anti-diagonal
      if (row + col === BOARD_SIZE - 1) {
        for (let i = 0; i < BOARD_SIZE; i++) {
          if (this.board[i][(BOARD_SIZE - 1) - i] !== player)
            break;

          if (i === BOARD_SIZE - 1)
            return true;
        }
      }

      return false;
    },
    checkDraw() {
      return this.moveCount === BOARD_SIZE * BOARD_SIZE - 1;
    },
    playAgain() {
      Object.assign(this.$data, initialState());
    }
  },
  computed: {
    currentTurn() {
      if (this.xTurn)
        return "It's X's turn!";
      else
        return "It's O's turn!";
    },
  },
  components: {
    'board': Board
  }
};
</script>

<style>
.wrapper {
  display: table;
  margin: 0 auto;
}

.instructions {
  margin-top: 20px;
  text-align: center;
  font-size: 50px;
  font-weight: 500;
  color: #fff;
  text-shadow: 1px 1px 1px #000;
}

button {
  font-size: 35px;
  padding: 15px 20px;
  border: none;
  background-color: #6c7a89;
  display: block;
  margin: 0 auto;
  margin-top: 20px;
  color: #fff;
  font-weight: 600;
  cursor: pointer;
}

button:hover {
  opacity: .8;
}

@media (max-width: 500px) {
  .instructions {
    font-size: 35px;
  }
}
</style>
