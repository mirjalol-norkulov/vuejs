<template>
  <div class="tic-tac">
    <button
      ref="button"
      v-for="(btn, index) in buttons"
      :key="index"
      class="tic-tac__btn"
      @click="handleClick(index)"
    >{{ btn }}</button>
  </div>
</template>

<script>
const X = "X"
const O = "O"
const EMPTY = " "

export default {
  name: "TicTacToe",
  data() {
    return {
      turn: X,
      buttons: [
        EMPTY, EMPTY, EMPTY,
        EMPTY, EMPTY, EMPTY,
        EMPTY, EMPTY, EMPTY
      ],
      winningLines: [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
      ],
      clicksCount: 0,
      object: {
        property: 10
      }
    }
  },
  methods: {
    handleClick(index) {
      // this.buttons[index] = this.turn; not works in Vue 2
      this.$set(this.buttons, index, this.turn);

      // this.$set(this.object, property, 15);
      this.turn = this.turn === X ? O : X;

      this.clicksCount++;

      if (this.clicksCount >= 5) {
        this.checkForWin();
      }
    },
    checkForWin() {
      const isXWon = this.winningLines.some(line => line.every(index => this.buttons[index] === X));
      const isOWon = this.winningLines.some(line => line.every(index => this.buttons[index] === O));


      if (isXWon) {
        setTimeout(() => {
          alert('X yutdi!')
        }, 100);
      }

      if (isOWon) {
        alert('O yutdi!')
      }

      if (this.clicksCount === 9) {
        alert('Durrang!')
      }

    }
  }
}
</script>

<style lang="scss">
.tic-tac {
  display: grid;
  grid-template-columns: repeat(3, 200px);
  grid-template-rows: repeat(3, 200px);

  .tic-tac__btn {
    font-size: 48px;
  }
}
</style>