<template>
	<div>
		<button v-on:click="shuffleTiles">Shuffle</button>
		<div
			class="zwipe"
			:style="{
				'--columns': this.columns,
				'--rows': this.rows
			}"
		>
			<template v-for="(tilesRow, rowIndex) in tilesArray">
				<Tile
					v-for="(tile, columnIndex) in tilesRow"
					:key="'row-' + rowIndex + '-column-' + columnIndex"
					@click-tile="clickTile(rowIndex, columnIndex)"
					:class="{ blank: tile.isBlank }"
					v-bind:styles="{
						positionRow: tile.positionRow,
						positionColumn: tile.positionColumn,
						backgroundRow: tile.backgroundRow,
						backgroundColumn: tile.backgroundColumn
					}"
				/>
			</template>
		</div>
	</div>
</template>

<script>
import Tile from '@/components/tile.vue';

export default {
	components: {
		Tile
	},
	data() {
		return {
			columns: 5,
			rows: 5,
			columnBlank: 0,
			rowBlank: 0,
			addressArray: [],
			tilesArray: []
		};
	},
	created() {
		this.createTiles();
		// this.shuffleTiles();
	},
	methods: {
		createTiles() {
			console.log('createTiles');

			let tilesArrayCopy = [];
			let addressArrayCopy = [];
			for (let i = 0; i < this.rows; i++) {
				tilesArrayCopy.push([]);
				addressArrayCopy.push([]);
				for (let j = 0; j < this.columns; j++) {
					let isBlank = i === this.rows - 1 && j === this.columns - 1;
					tilesArrayCopy[i].push({
						positionRow: i,
						positionColumn: j,
						backgroundRow: !isBlank ? i : -1,
						backgroundColumn: !isBlank ? j : -1,
						isBlank: isBlank
					});
					addressArrayCopy[i].push({
						rowIndex: i,
						columnIndex: j
					});
				}
			}

			this.rowBlank = this.rows - 1;
			this.columnBlank = this.columns - 1;

			this.addressArray = addressArrayCopy;
			this.tilesArray = tilesArrayCopy;
			return true;
		},
		clickTile(rowIndex, columnIndex) {
			let correctRow = this.addressArray[rowIndex][columnIndex]['rowIndex'] === this.rowBlank;
			let correctColumn = this.addressArray[rowIndex][columnIndex]['columnIndex'] === this.columnBlank;
			if (!correctRow && !correctColumn) {
				return false;
			} else if (correctRow && correctColumn) {
				alert('user is sus vote them out');
				return false;
			} else if (correctRow) {
				console.log('woo row');
				if (columnIndex > this.columnBlank) {
					for (let i = this.columnBlank + 1; i <= columnIndex; i++) {
						const thisTile = this.tilesArray[rowIndex][i];
						this.$set(this.tilesArray[rowIndex], i - 1, thisTile);
					}
				} else {
					for (let i = this.columnBlank - 1; i >= columnIndex; i--) {
						const thisTile = this.tilesArray[rowIndex][i];
						this.$set(this.tilesArray[rowIndex], i + 1, thisTile);
					}
				}
			} else if (correctColumn) {
				console.log('woo column');
				if (rowIndex > this.rowBlank) {
					for (let i = this.rowBlank + 1; i <= rowIndex; i++) {
						const thisTile = this.tilesArray[i][columnIndex];
						this.$set(this.tilesArray[i - 1], columnIndex, thisTile);
					}
				} else {
					for (let i = this.rowBlank - 1; i >= rowIndex; i--) {
						const thisTile = this.tilesArray[i][columnIndex];
						this.$set(this.tilesArray[i + 1], columnIndex, thisTile);
					}
				}
			}
			this.rowBlank = rowIndex;
			this.columnBlank = columnIndex;
			// return false;
			// if ((rowIndex === this.rowBlank && columnIndex === this.columnBlank) || (rowIndex !== this.rowBlank && columnIndex !== this.columnBlank)) {
			// 	console.log('null');
			// 	return false;
			// } else {
			// 	if (rowIndex === this.rowBlank) {
			// 		if (columnIndex > this.columnBlank) {
			// 			for (let i = this.columnBlank + 1; i <= columnIndex; i++) {
			// 				const thisTile = this.tilesArray[rowIndex][i];
			// 				this.$set(this.tilesArray[rowIndex], i - 1, thisTile);
			// 			}
			// 		} else {
			// 			for (let i = this.columnBlank - 1; i >= columnIndex; i--) {
			// 				const thisTile = this.tilesArray[rowIndex][i];
			// 				this.$set(this.tilesArray[rowIndex], i + 1, thisTile);
			// 			}
			// 		}
			// 	}
			// 	if (columnIndex === this.columnBlank) {
			// 		if (rowIndex > this.rowBlank) {
			// 			for (let i = this.rowBlank + 1; i <= rowIndex; i++) {
			// 				const thisTile = this.tilesArray[i][columnIndex];
			// 				this.$set(this.tilesArray[i - 1], columnIndex, thisTile);
			// 			}
			// 		} else {
			// 			for (let i = this.rowBlank - 1; i >= rowIndex; i--) {
			// 				const thisTile = this.tilesArray[i][columnIndex];
			// 				this.$set(this.tilesArray[i + 1], columnIndex, thisTile);
			// 			}
			// 		}
			// 	}
			// 	this.$set(this.tilesArray[rowIndex], columnIndex, null);
			// 	this.rowBlank = rowIndex;
			// 	this.columnBlank = columnIndex;
			// }
		},
		shuffleTiles() {
			console.log('shuffleTiles');
			var tilesArrayCopy = JSON.parse(JSON.stringify(this.tilesArray));
			tilesArrayCopy.forEach((row, rowIndex) => {
				row.forEach((tile, columnIndex) => {
					let newRowIndex = Math.floor(Math.random() * this.rows);
					let newColumnIndex = Math.floor(Math.random() * this.columns);

					let newTile = JSON.parse(JSON.stringify(tilesArrayCopy[newRowIndex][newColumnIndex]));

					this.$set(this.tilesArray[newRowIndex][newColumnIndex], 'positionRow', tile.positionRow);
					tilesArrayCopy[newRowIndex][newColumnIndex].positionRow = tile.positionRow;
					this.$set(this.tilesArray[newRowIndex][newColumnIndex], 'positionColumn', tile.positionColumn);
					tilesArrayCopy[newRowIndex][newColumnIndex].positionColumn = tile.positionColumn;

					this.$set(this.tilesArray[rowIndex][columnIndex], 'positionRow', newTile.positionRow);
					tilesArrayCopy[rowIndex][columnIndex].positionRow = newTile.positionRow;
					this.$set(this.tilesArray[rowIndex][columnIndex], 'positionColumn', newTile.positionColumn);
					tilesArrayCopy[rowIndex][columnIndex].positionColumn = newTile.positionColumn;

					if (tile.isBlank) {
						this.rowBlank = tile.positionRow;
						this.columnBlank = tile.positionColumn;
					} else if (newTile.isBlank) {
						this.rowBlank = newTile.positionRow;
						this.columnBlank = newTile.positionColumn;
					}

					[this.addressArray[rowIndex][columnIndex], this.addressArray[newRowIndex][newColumnIndex]] = [this.addressArray[newRowIndex][newColumnIndex], this.addressArray[rowIndex][columnIndex]];
				});
			});
		}
	}
};
</script>

<style lang="scss" scoped>
.zwipe {
	background: #ffffff;
	width: 320px;
	height: 320px;
	margin: 0 auto;
	position: relative;
}
button {
	display: block;
	margin: 10px auto;
}
</style>
