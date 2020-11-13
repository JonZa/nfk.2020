<template>
	<div>
		<nuxt />
		<app-nav />
	</div>
</template>

<script>
import AppNav from '~/components/AppNav.vue';

export default {
	components: {
		AppNav
	}
};
</script>

<style lang="scss">
@import '@/assets/mixins.scss';

*,
*:before,
*:after {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}
html {
	font-family: sans-serif;
	font-size: 100%;
	word-spacing: 1px;
	box-sizing: border-box;
}
body {
	background-color: #22222a;
	background-repeat: no-repeat;
	padding: 100px 35px;
	color: #fff;
	&::after,
	&::before {
		display: block;
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		padding-top: 56.25%;
		z-index: -1;
	}
	&::before {
		@include background-image('/me-mobile', 'jpg', 100%, auto);
	}
	&::after {
		background: linear-gradient(to top, #22222a, transparent);
	}
}
h1 {
	font-family: 'Nunito';
	font-size: 36px;
	line-height: 45px;
	transform: translateY(-5px);
	padding-top: 1px;
	margin-bottom: 20px;
}
h2 {
	font-family: 'Nunito';
	font-size: 24px;
	line-height: 30px;
	transform: translateY(-1px);
	padding-top: 1px;
}
h3 {
	font-family: 'Nunito';
	font-size: 20px;
	line-height: 25px;
	transform: translateY(-3px);
	padding-top: 1px;
}
h2,
h3,
p {
	margin-bottom: 15px;
}
p {
	padding-bottom: 0;
	font-size: 1.125rem;
	line-height: 25px;
	transform: translateY(-3px);
	padding-top: 1px;
	font-family: 'Alegreya';
}

#{$a-tags} {
	color: #ff99cc;
	text-decoration: underline;
}
#{$a-tags-hover} {
	color: #ff99cc;
	text-decoration: none;
}
strong {
	font-weight: normal;
	color: #95d2e4;
}
</style>
