<template>
  <div class="board" v-if="squares">
    <div v-for="row in 3" :key="row" class="board-row">
      <Square
        v-for="i in 3"
        :key="indexByRow(i, row)"
        :value="squares[indexByRow(i, row)]"
        :disabled="!!winner"
        :winner="!!winner && winner.includes(indexByRow(i, row))"
        @click="click(i, row)"
      />
    </div>
  </div>
</template>

<script>
import Square from './Square.vue';
export default {
  name: 'Board',
  props: {
    squares: Array,
    winner: Array,
  },
  components: { Square },
  methods: {
    indexByRow(index, row, max = 3) {
      return row * max + index - (max + 1);
    },

    click(index, row) {
      this.$emit('click', this.indexByRow(index, row));
    },
  },
};
</script>

<style scoped>
.board {
  border: 1rem solid #fff4;
  box-shadow: 2.5px 5px 25px #0004, 0 1px 6px #0006;
  border-radius: 0.5rem;
  width: 65vmin;
  height: 65vmin;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: repeat(3, 1fr);
  background-color: lightblue;
}

.board-row {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 1fr;
}
</style>
