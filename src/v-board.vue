<template>
  <div class="board" :class="{'scale': isScale}">
    <div class="row">
      <div class="cell header-cell">
        <div class="cell-ration">
          <button
            type="button"
            class="cell-content scale-button"
            @click="scaleBoard()"
          >
            s
          </button>
        </div>
      </div>

      <div
        v-for="col in cols"
        :key="col"
        class="cell header-cell"
      >
        <div class="cell-ration">
          <div class="cell-content">
            {{col}}
          </div>
        </div>
      </div>
    </div>

    <div
      v-for="(row, i) of rows"
      :key="`row-${i}`"
      class="row"
    >
      <div class="cell header-cell">
        <div class="cell-ration">
          <div class="cell-content">
            {{row}}
          </div>
        </div>
      </div>

      <div
        v-for="(col, j) of cols"
        :key="`col-${j}`"
        class="cell"
      >
        <div class="cell-ration">
          <button
            class="cell-content"
            type="button"
            @click="$emit('click-cell', {col, row})"
          >
            {{ matrix[j][i] }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VBoard',
  props: {
    cols: { type: Array, required: true },
    rows: { type: Array, required: true },
  },
  data: () => ({
    matrix: null,
    isScale: false,
  }),
  created() {
    this.matrix = this.createGrid(this.cols.length, this.rows.length);

    for (let i = 0; i < this.cols.length; i++) {
      for (let j = 0; j < this.rows.length; j++) {
        this.matrix[i][j] = `${this.cols[i]}${this.rows[j]}`;
      }
    }
  },
  methods: {
    createGrid(cols, rows) {
      const matrix = new Array(cols);

      for (let i = 0; i < matrix.length; i++) {
        matrix[i] = new Array(rows);
      }

      return matrix;
    },
    scaleBoard() {
      this.isScale = !this.isScale;
    },
  },
};
</script>

<style scoped>
.board {
  position: relative;
}

.scale {
  transform: scale(2) translate3d(25%, 25%, 0);
}

.row {
  display: flex;
}

.row:last-child .cell:not(:first-child) {
  border-bottom: 1px solid #ccc;
}

.row:not(:first-child) .cell:last-child {
  border-right: 1px solid #ccc;
}

.cell {
  position: relative;
  flex: 1;
  min-width: 30px;
  border-top: 1px solid #ccc;
  border-left: 1px solid #ccc;
}

.header-cell {
  border: 0;
}

.cell-content[type="button"]:not(.scale-button) {
  border: 0;
  background: transparent;
  outline: transparent;
  cursor: pointer;
}

.cell-ration {
  padding-top: 100%;
  height: 0;
}

.cell-content {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

.scale-button {
  border: 0;
  background-color: transparent;
  outline: transparent;
  cursor: pointer;
}
</style>
