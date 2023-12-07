<template>
    <div class="game-board">
      <div v-for="(row, rowIndex) in board" :key="rowIndex" class="row">
        <div v-for="(cell, colIndex) in row" :key="colIndex" class="cell" @click="makeMove(rowIndex, colIndex)">
          {{ cell }}
        </div>
      </div>
      <div v-if="winner">
        <p>Player {{ winner }} wins!</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        board: [
          ['', '', ''],
          ['', '', ''],
          ['', '', '']
        ],
        currentPlayer: 'X',
        isOver: false,
        winner: null
      };
    },
    methods: {
      makeMove(row, col) {
        if(this.winner){
            return;
        }

        if (this.board[row][col] === '' && !this.isOver) {
                this.board[row][col] = this.currentPlayer;
          if (this.checkWinner(row, col, this.currentPlayer)) {
            this.winner = this.currentPlayer;
          } else {
            this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
          }
        }
      },
      checkWinner(row, col, player) {
        // Check for a winner
        // Implement your logic to check rows, columns, and diagonals for a win
        // You may want to use a separate function for each check

        // Check row
        if (this.board[row].every((cell) => cell === player)) {
        return true;
        }

        // Check column
        if (this.board.every((row) => row[col] === player)) {
        return true;
        }

        // Check diagonal from top-left to bottom-right
        if (row === col && this.board.every((row, index) => row[index] === player)) {
        return true;
        }

        // Check diagonal from top-right to bottom-left
        if (row + col === this.board.length - 1 && this.board.every((row, index) => row[this.board.length - 1 - index] === player)) {
        return true;
        }

        return false;
        } 
    }
  };
  </script>
  
  <style scoped>
  /* Add styling for the game board and cells */
  .game-board {
    display: grid;
    justify-content: center;
    /* align-items: center; */
    margin-top:25vh;
  }
  
  .row {
    display: flex;
  }
  
  .cell {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 50px;
    border: 1px solid #ccc;
    width: 100px;
    height: 100px; /* Adjust the height as needed */
    cursor: pointer;
  }
  
  /* Add more styling as needed */
  </style>
  