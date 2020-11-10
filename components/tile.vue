<template>
	<div
		class="tile"
		@click="$emit('click-tile')"
		:style="{
			'--currentRow': styles.currentRow,
			'--currentColumn': styles.currentColumn,
			'--startRow': styles.startRow,
			'--startColumn': styles.startColumn
		}"
	/>
</template>

<script>
export default {
	props: {
		styles: {
			currentRow: Number,
			currentColumn: Number,
			startRow: Number,
			startColumn: Number
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
	width: 64px;
	height: 64px;
	cursor: pointer;
	background-image: url('/cat-320x320.jpg');
	background-repeat: no-repeat;
	position: absolute;
	top: 0;
	left: 0;
	--startColumn: 0;
	--startRow: 0;
	--currentColumn: 0;
	--currentRow: 0;
	background-position: calc(-1 * 64px * var(--startColumn))
		calc(-1 * 64px * var(--startRow));
	transform: translate(
		calc(64px * var(--currentColumn)),
		calc(64px * var(--currentRow))
	);
	transition: transform 0.3s cubic-bezier(0.16, 1, 0.3, 1);
	&.blank {
		background: transparent;
		box-shadow: none;
		pointer-events: none;
	}
}
</style>
