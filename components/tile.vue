<template>
	<button
		type="button"
		class="tile"
		@mousedown="$emit('click-tile')"
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
@import '@/assets/mixins.scss';
.tile {
	border: 0;
	padding: 0;
	box-shadow: inset 1px 1px 2px rgba(255, 255, 255, 0.75), inset -1px -1px 2px rgba(0, 0, 0, 0.5);
	border-radius: 4px;
	width: 80px;
	height: 80px;
	cursor: pointer;
	// @include background-image('/banksy', 'png', 320px, 320px);
	background-image: url('~@/static/banksy.jpg?resize&size=320&format=webp');
	@media only screen and (-webkit-min-device-pixel-ratio: 2), only screen and (-moz-min-device-pixel-ratio: 2), only screen and (-o-min-device-pixel-ratio: 2/1), only screen and (min-device-pixel-ratio: 2), only screen and (min-resolution: 192dpi), only screen and (min-resolution: 2dppx) {
		background-image: url('~@/static/banksy.jpg?resize&size=640&format=webp');
		background-size: calc(var(--columns) * 100%);
	}
	background-repeat: no-repeat;
	position: absolute;
	top: 0;
	left: 0;
	outline: 0;
	--startColumn: 0;
	--startRow: 0;
	--currentColumn: 1.5;
	--currentRow: 1.5;
	background-position: calc(-1 * 80px * var(--startColumn)) calc(-1 * 80px * var(--startRow));
	transform: translate(calc(80px * var(--currentColumn)), calc(80px * var(--currentRow)));
	transition: transform 0.3s cubic-bezier(0.16, 1, 0.3, 1);
	&.blank {
		background: transparent;
		box-shadow: none;
		pointer-events: none;
	}
}
</style>
