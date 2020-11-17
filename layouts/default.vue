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
	components: {
		AppNav
	},
	methods: {
		toggleNavIsOpen() {
			console.log(this.navIsOpen);
			this.navIsOpen = !this.navIsOpen;
			console.log(this.navIsOpen);
		}
	}
};
</script>

<style lang="scss">
@import '@/assets/mixins.scss';
.open {
	outline: 10px solid #f00;
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
	background-color: #22222a;
	background-repeat: no-repeat;
	color: #fff;
}
.container {
	padding: 100px 30px 20px 30px;
	&::after,
	&::before {
		@include background-image('/me-mobile', jpg, 100%, auto, #22222a, transparent, 'to top');
		display: block;
		content: '';
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		padding-top: 56.25%;
		z-index: -1;
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
@keyframes glitch-anim {
	$steps: 10;
	@for $i from 0 through $steps {
		0% {
			clip: rect(0, 0, 0, 0);
		}
		59% {
			clip: rect(0, 0, 0, 0);
		}
		#{percentage(0.60 + $i*(0.30/$steps))} {
			left: -10 + random(20) + px;
			top: random(25) + px;
			clip: rect(random(75) + px, 9999px, random(125) + px, 0);
		}
	}
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
}
h1,
h2,
h3,
p,
ul {
	margin-bottom: 15px;
}
h2 {
	padding-top: 10px;
}
p,
li {
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

.content {
	transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
	transition-delay: 0.3s;
	@at-root .container--nav-is-open & {
		transition-delay: 0.15s;
		transform: translatex(calc(-100% - 35px));
	}
	#{$a-tags} {
		color: #ff99cc;
		box-shadow: inset 0 -1px 0 #ff99cc;
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
