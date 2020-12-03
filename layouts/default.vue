<template>
	<div class="container" :class="navIsOpen ? 'container--nav-is-open' : ''">
		<nuxt class="content" />
		<app-nav :navIsOpen="this.navIsOpen" @toggle-nav-is-open="toggleNavIsOpen" />
	</div>
</template>

<script>
import AppNav from '~/components/AppNav.vue';

export default {
	data() {
		return {
			navIsOpen: false
		};
	},
	mounted() {
		function testWebPSupport() {
			return new Promise(resolve => {
				const webp = 'data:image/webp;base64,UklGRkAAAABXRUJQVlA4WAoAAAAQAAAAAAAAAAAAQUxQSAIAAAAAAFZQOCAYAAAAMAEAnQEqAQABAAFAJiWkAANwAP79NmgA';
				const test_img = new Image();
				test_img.src = webp;
				test_img.onerror = e => resolve(false);
				test_img.onload = e => resolve(true);
			});
		}
		(async () => {
			const supports_webp = await testWebPSupport();
			// for stylesheets
			if (supports_webp) {
				document.body.classList.add('webp');
			}
		})();
	},
	components: {
		AppNav
	},
	methods: {
		toggleNavIsOpen() {
			this.navIsOpen = !this.navIsOpen;
		}
	}
};
</script>

<style lang="scss">
@import '@/assets/mixins.scss';
@import '@/assets/variables.scss';
/* nunito-900 - latin */
@font-face {
  font-family: 'Nunito';
  font-style: normal;
  font-weight: 900;
  src: url('~@/static/fonts/nunito-v16-latin-900.eot'); /* IE9 Compat Modes */
  src: local(''),
       url('~@/static/fonts/nunito-v16-latin-900.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
       url('~@/static/fonts/nunito-v16-latin-900.woff2') format('woff2'), /* Super Modern Browsers */
       url('~@/static/fonts/nunito-v16-latin-900.woff') format('woff'), /* Modern Browsers */
       url('~@/static/fonts/nunito-v16-latin-900.ttf') format('truetype'), /* Safari, Android, iOS */
       url('~@/static/fonts/nunito-v16-latin-900.svg#Nunito') format('svg'); /* Legacy iOS */
}
/* alegreya-regular - latin */
@font-face {
  font-family: 'Alegreya';
  font-style: normal;
  font-weight: 400;
  src: url('~@/static/fonts/alegreya-v16-latin-regular.eot'); /* IE9 Compat Modes */
  src: local(''),
       url('~@/static/fonts/alegreya-v16-latin-regular.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
       url('~@/static/fonts/alegreya-v16-latin-regular.woff2') format('woff2'), /* Super Modern Browsers */
       url('~@/static/fonts/alegreya-v16-latin-regular.woff') format('woff'), /* Modern Browsers */
       url('~@/static/fonts/alegreya-v16-latin-regular.ttf') format('truetype'), /* Safari, Android, iOS */
       url('~@/static/fonts/alegreya-v16-latin-regular.svg#Alegreya') format('svg'); /* Legacy iOS */
}
*,
*:before,
*:after {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}
html {
	font-family: 'Alegreya', serif;
	font-size: 100%;
	word-spacing: 1px;
	box-sizing: border-box;
}
body {
	background-color: $shark;
	background-repeat: no-repeat;
	color: #fff;
}
.container {
	padding: 100px 0 50px 0;
	margin: 0 auto;
	width: calc(100% - 40px);
	max-width: 570px;
	min-width: 320px;
	&::after,
	&::before {
		display: block;
		content: '';
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		padding-top: 56.25%;
		z-index: -1;
		background-image: linear-gradient(to top, $shark, transparent), url('~@/static/me.jpg?resize&size=480&format=webp');
		@media only screen and (-webkit-min-device-pixel-ratio: 2), only screen and (-moz-min-device-pixel-ratio: 2), only screen and (-o-min-device-pixel-ratio: 2/1), only screen and (min-device-pixel-ratio: 2), only screen and (min-resolution: 192dpi), only screen and (min-resolution: 2dppx) {
			background-image: linear-gradient(to top, $shark, transparent), url('~@/static/me.jpg?resize&size=960&format=webp');
		}
		@include bp(desktop) {
			display: none;
		}
	}
	&::after {
		filter: hue-rotate(90deg);
		clip: rect(0, 0, 0, 0);
		opacity: 0;
		transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
	}
	&--nav-is-open::after {
		opacity: 1;
		left: -10px;
		animation: glitch-anim 5s linear infinite alternate;
	}
}
h1 {
	font-family: 'Nunito';
	font-size: 36px;
	line-height: 45px;
	transform: translateY(-5px);
	padding-top: 1px;
	margin-bottom: 20px;
	transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
	position: relative;
	&:before,
	&:after {
		content: attr(title);
		position: absolute;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		overflow: hidden;
	}
}
h2 {
	font-family: 'Nunito';
	font-size: 24px;
	line-height: 30px;
	transform: translateY(-1px);
	padding-top: 1px;
	color: lighten(#95d2e4, 10%);
	small {
		color: mix(#fff, lighten($shark, 10%));
	}
}
h3 {
	font-size: 20px;
	line-height: 25px;
	margin-bottom: 20px;
	transform: translateY(-3px);
	font-weight: normal;
}
h1,
h2,
h3,
p,
ul,
blockquote {
	margin-bottom: 20px;
}
ul {
	padding-left: 25px;
}
p,
li,
blockquote {
	font-size: 1.125rem;
	line-height: 25px;
	transform: translateY(-3px);
	padding-top: 1px;
}
.list {
	&--plain {
		list-style-type: none;
	}
}
li {
	margin-bottom: 5px;
}
button {
	font-family: 'Nunito';
	cursor: pointer;
}
img {
	max-width: 100%;
}
hr {
	height: 17px;
	border: 0;
	margin-bottom: 25px;
	position: relative;
	background-repeat: no-repeat;
	background-position: center;
	background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 217 17' fill='none' xmlns='http://www.w3.org/2000/svg'%3E %3Crect x='50' y='13.4351' width='19' height='5' rx='2.5' transform='rotate(-45 50 13.4351)' fill='%23FF99CC' fill-opacity='0.33'/%3E %3Crect x='63.4351' y='16.9706' width='19' height='5' rx='2.5' transform='rotate(-135 63.4351 16.9706)' fill='%23FF99CC' fill-opacity='0.33'/%3E %3Crect x='100' y='13.4351' width='19' height='5' rx='2.5' transform='rotate(-45 100 13.4351)' fill='%23FF99CC' fill-opacity='0.5'/%3E %3Crect x='113.435' y='16.9706' width='19' height='5' rx='2.5' transform='rotate(-135 113.435 16.9706)' fill='%23FF99CC' fill-opacity='0.5'/%3E %3Crect y='13.4351' width='19' height='5' rx='2.5' transform='rotate(-45 0 13.4351)' fill='%23FF99CC' fill-opacity='0.16'/%3E %3Crect x='13.4351' y='16.9706' width='19' height='5' rx='2.5' transform='rotate(-135 13.4351 16.9706)' fill='%23FF99CC' fill-opacity='0.16'/%3E %3Crect x='150' y='13.4351' width='19' height='5' rx='2.5' transform='rotate(-45 150 13.4351)' fill='%23FF99CC' fill-opacity='0.33'/%3E %3Crect x='163.435' y='16.9706' width='19' height='5' rx='2.5' transform='rotate(-135 163.435 16.9706)' fill='%23FF99CC' fill-opacity='0.33'/%3E %3Crect x='200' y='13.4351' width='19' height='5' rx='2.5' transform='rotate(-45 200 13.4351)' fill='%23FF99CC' fill-opacity='0.16'/%3E %3Crect x='213.435' y='16.9706' width='19' height='5' rx='2.5' transform='rotate(-135 213.435 16.9706)' fill='%23FF99CC' fill-opacity='0.16'/%3E %3C/svg%3E ");
}

.page-enter-active {
	animation: pageAnimation 0.35s;
}
.page-leave-active {
	animation: pageAnimation backwards 0.35s;
}

@keyframes pageAnimation {
	0% {
		opacity: 0;
	}
	12.5% {
		opacity: 0.25;
		filter: blur(2px);
	}
	25% {
		opacity: 0;
	}
	37.5% {
		opacity: 0;
	}
	50% {
		opacity: 0.75;
		filter: blur(7px);
	}
	62.5% {
		opacity: 0;
	}
	75% {
		opacity: 0.25;
		filter: blur(2px);
	}
	87.5% {
		opacity: 0.5;
		filter: blur(5px);
	}
	100% {
		opacity: 1;
	}
}
.content {
	max-width: 570px;
	transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
	@at-root .container--nav-is-open & {
		opacity: 0.25;
		filter: blur(1px);
	}
	#{$a-tags} {
		color: $carnation;
		box-shadow: inset 0 -1px 0 $carnation;
		text-decoration: none;
		transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
	}
	#{$a-tags-hover} {
		color: #fff;
		box-shadow: inset 0 -1px 0 #fff;
	}
}
strong {
	font-weight: normal;
	color: #95d2e4;
}
blockquote {
	p {
		margin-bottom: 10px;
		&:last-of-type {
			margin-bottom: 5px;
		}
	}
}
cite {
	font-style: normal;
	color: #95d2e4;
	display: block;
}

.icon {
	&--big {
		height: 54px;
		@at-root .columns--icons & {
			position: absolute;
			top: 0;
			left: 0;
		}
	}
	&--inline {
		height: 18px;
		transform: translatey(3px);
		margin-right: 5px;
	}
	path {
		fill: #fff;
	}
}

.columns {
	display: flex;
	.child {
		flex: 1 1 50%;
	}
	&--icons {
		.child {
			position: relative;
			padding-left: 80px;
		}
	}
}
</style>
