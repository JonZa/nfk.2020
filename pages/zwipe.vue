<template>
  <div class="zwipe">
    <button v-on:click="shuffleTiles">Shuffle</button>
    <br />
    <div v-for="(tilesRow, rowIndex) in tilesArray" :key="rowIndex">
      <template v-for="(tilesColumn, columnIndex) in tilesRow">
        <input
          type="text"
          :value="tilesColumn"
          :key="columnIndex"
          readonly
          v-on:click="clickTile(rowIndex, columnIndex)"
        />
      </template>
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
        ["a", "b", "c", "d", "e"],
        ["f", "g", "h", "i", "j"],
        ["k", "l", "m", "n", "o"],
        ["p", "q", "r", "s", "t"],
        ["u", "v", "w", "x", null]
      ]
    };
  },
  created() {
    this.shuffleTiles();
  },
  methods: {
    clickTile(rowIndex, columnIndex) {
      if ((rowIndex === this.rowNull && columnIndex === this.columnNull) || rowIndex !== this.rowNull && columnIndex !== this.columnNull) {
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
input {
  width: 64px;
  line-height: 64px;
  text-align: center;
  font-size: 25px;
  font-weight: bold;
}
</style>
