<template>
  <div class="zwipe">
    <button v-on:click="shuffleTiles">Shuffle</button>
    <br />
    <div class="row" v-for="(tilesRow, rowIndex) in tilesArray" :key="rowIndex">
      <div
        v-for="(tile, columnIndex) in tilesRow"
        :key="columnIndex"
        v-on:click="clickTile(rowIndex, columnIndex)"
        class="tile"
        :style="[
          tile !== null
            ? { '--tileRow': tile[0], '--tileColumn': tile[1] }
            : { background: 'none' }
        ]"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      columnNull: 0,
      rowNull: 0,
      tilesArray: [
        [
          [0, 0],
          [0, 1],
          [0, 2],
          [0, 3],
          [0, 4]
        ],
        [
          [1, 0],
          [1, 1],
          [1, 2],
          [1, 3],
          [1, 4]
        ],
        [
          [2, 0],
          [2, 1],
          [2, 2],
          [2, 3],
          [2, 4]
        ],
        [
          [3, 0],
          [3, 1],
          [3, 2],
          [3, 3],
          [3, 4]
        ],
        [[4, 0], [4, 1], [4, 2], [4, 3], null]
      ]
    };
  },
  created() {
    this.shuffleTiles();
  },
  methods: {
    clickTile(rowIndex, columnIndex) {
      if (
        (rowIndex === this.rowNull && columnIndex === this.columnNull) ||
        (rowIndex !== this.rowNull && columnIndex !== this.columnNull)
      ) {
        return false;
      } else {
        if (rowIndex === this.rowNull) {
          if (columnIndex > this.columnNull) {
            for (let i = this.columnNull + 1; i <= columnIndex; i++) {
              const thisTile = this.tilesArray[rowIndex][i];
              this.$set(this.tilesArray[rowIndex], i - 1, thisTile);
            }
          } else {
            for (let i = this.columnNull - 1; i >= columnIndex; i--) {
              const thisTile = this.tilesArray[rowIndex][i];
              this.$set(this.tilesArray[rowIndex], i + 1, thisTile);
            }
          }
        }
        if (columnIndex === this.columnNull) {
          if (rowIndex > this.rowNull) {
            for (let i = this.rowNull + 1; i <= rowIndex; i++) {
              const thisTile = this.tilesArray[i][columnIndex];
              this.$set(this.tilesArray[i - 1], columnIndex, thisTile);
            }
          } else {
            for (let i = this.rowNull - 1; i >= rowIndex; i--) {
              const thisTile = this.tilesArray[i][columnIndex];
              this.$set(this.tilesArray[i + 1], columnIndex, thisTile);
            }
          }
        }
        this.$set(this.tilesArray[rowIndex], columnIndex, null);
        this.rowNull = rowIndex;
        this.columnNull = columnIndex;
      }
    },
    shuffleTiles() {
      var tilesArrayCopy = this.tilesArray;

      var tilesRows = tilesArrayCopy.length;
      var tilesColumns = tilesArrayCopy[0].length;

      tilesArrayCopy.forEach((tilesRow, thisRow) => {
        tilesRow.forEach((thisTile, thisColumn) => {
          var newRow = Math.floor(Math.random() * tilesRows);
          var newColumn = Math.floor(Math.random() * tilesColumns);

          var otherTile = this.tilesArray[newRow][newColumn];

          if (thisTile === null) {
            this.rowNull = newRow;
            this.columnNull = newColumn;
          }
          if (otherTile === null) {
            this.rowNull = thisRow;
            this.columnNull = thisColumn;
          }

          this.$set(this.tilesArray[newRow], newColumn, thisTile);
          this.$set(this.tilesArray[thisRow], thisColumn, otherTile);
        });
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.zwipe {
  background: #eee;
  width: 320px;
  margin: 0 auto;
}
button {
  margin: 10px;
}
.zwipe .row {
  display: flex;
}
.zwipe .tile {
  width: 64px;
  height: 64px;
  cursor: pointer;
  outline: 1px solid rgba(255,255,255,0.5);
  background-image: url("/cat-320x320.jpg");
  background-position: calc(-64px * var(--tileColumn))
    calc(-64px * var(--tileRow));
}
</style>
