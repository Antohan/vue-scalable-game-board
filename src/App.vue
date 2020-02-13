<template>
  <div id="app">
    <div class="border-container">
      <v-board
        :cols="cols"
        :rows="rows"
        @click-cell="onClickCell"
      />
    </div>

    <h1>
      {{ selectCell }}
    </h1>
  </div>
</template>

<script>
import VBoard from './v-board';

export default {
  name: "App",
  components: {
    VBoard,
  },
  data: () => ({
    cols: ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j'],
    rows: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    selectCell: null,
  }),
  methods: {
    onClickCell({ col, row }) {
      this.selectCell = `${col}${row}`;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0 auto;
  max-width: 1200px;
  width: 100%;
}

.border-container {
  max-width: 640px;
  margin: 0 auto;
  overflow: auto;
}
</style>
