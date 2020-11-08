<template>
	<div
		class="tile"
		@click="$emit('click-tile')"
		:style="{
			'--position-row': styles.positionRow,
			'--position-column': styles.positionColumn,
			'--background-row': styles.backgroundRow,
			'--background-column': styles.backgroundColumn
		}"
	/>
</template>

<script>
export default {
	props: {
		styles: {
			positionRow: Number,
			positionColumn: Number,
			backgroundRow: Number,
			backgroundColumn: Number
		}
	}
};
</script>

<style lang="scss">
.tile {
	box-shadow: inset 1px 1px 2px rgba(255, 255, 255, 0.5),
		inset -1px -1px 2px rgba(0, 0, 0, 0.25);
	border-radius: 4px;
	outline-offset: -1px;
	--width: calc(100% / var(--columns));
	--height: calc(100% / var(--rows));
	width: var(--width);
	height: var(--height);
	cursor: pointer;
	background-image: url('/cat-320x320.jpg');
	background-repeat: no-repeat;
	position: absolute;
	top: 0;
	left: 0;
	--background-column: 0;
	--background-row: 0;
	--position-column: 0;
	--position-row: 0;
	background-position: calc(-1 * 64px * var(--background-column))
		calc(-1 * 64px * var(--background-row));
	transform: translate(
		calc(64px * var(--position-column)),
		calc(64px * var(--position-row))
	);
	transition: transform 0.3s cubic-bezier(0.16, 1, 0.3, 1);
	&.blank {
		background: transparent;
		box-shadow: none;
		pointer-events: none;
	}
}
</style>
