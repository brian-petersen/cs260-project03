<template>
  <table>
    <tr>
      <td>
        <div class="square" @click="squareClick(0, 0)">{{ board[0][0] }}</div>
      </td>
      <td>
        <div class="square" @click="squareClick(0, 1)">{{ board[0][1] }}</div>
      </td>
      <td>
        <div class="square" @click="squareClick(0, 2)">{{ board[0][2] }}</div>
      </td>
    </tr>
    <tr>
      <td>
        <div class="square" @click="squareClick(1, 0)">{{ board[1][0] }}</div>
      </td>
      <td>
        <div class="square" @click="squareClick(1, 1)">{{ board[1][1] }}</div>
      </td>
      <td>
        <div class="square" @click="squareClick(1, 2)">{{ board[1][2] }}</div>
      </td>
    </tr>
    <tr>
      <td>
        <div class="square" @click="squareClick(2, 0)">{{ board[2][0] }}</div>
      </td>
      <td>
        <div class="square" @click="squareClick(2, 1)">{{ board[2][1] }}</div>
      </td>
      <td>
        <div class="square" @click="squareClick(2, 2)">{{ board[2][2] }}</div>
      </td>
    </tr>
  </table>
</template>

<script>
export default {
  props: ['board'],
  methods: {
    squareClick(row, col) {
      this.$emit('click', row, col);
    }
  }
};
</script>

<style scoped>
.square {
  width: 150px;
  height: 150px;
  background: #6c7a89;
  cursor: pointer;
  font-size: 130px;
  line-height: 140px;
  text-align: center;
  color: #fff;
}

.square:hover {
  opacity: 0.8;
}

@media(max-width: 500px) {
  .square {
    width: 100px;
    height: 100px;
    font-size: 80px;
    line-height: 100px;
  }
}
</style>
