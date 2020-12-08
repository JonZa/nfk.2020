<template>
	<nav class="nav__container" :class="navIsOpen ? 'nav__container--open' : ''" @click="$emit('toggle-nav-is-open')">
		<button class="nav__hamburger" :class="navIsOpen ? 'nav__hamburger--open' : ''" type="button" aria-label="Show navigation"></button>
		<ul class="nav__links" :class="navIsOpen ? 'nav__links--open' : ''" :style="{ '--children': links.length }">
			<li v-for="(link, i) in links" :key="'link-' + i" :style="{ '--child-n': i + 1 }">
				<nuxt-link :to="link.to">{{ link.title }}</nuxt-link>
			</li>
		</ul>
	</nav>
</template>

<script>
export default {
	props: {
		navIsOpen: Boolean
	},
	data() {
		return {
			isOpen: false,
			links: [
				{
					title: 'Home',
					to: '/'
				},
				{
					title: 'About',
					to: '/about/'
				},
				{
					title: 'Experience',
					to: '/experience/'
				},
				{
					title: 'Endorsements',
					to: '/endorsements/'
				},
				{
					title: 'Contact',
					to: '/contact/'
				},
				{
					title: 'Game',
					to: '/game/'
				}
			]
		};
	}
};
</script>

<style lang="scss">
@import '@/assets/variables.scss';
@import '@/assets/mixins.scss';
@import '@/assets/include-media.scss';
.nav {
	&__container {
		@include media('<desktop') {
			&::before {
				display: block;
				pointer-events: none;
				content: '';
				position: fixed;
				right: 0;
				bottom: 0;
				width: 150px;
				height: 150px;
				transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
				background-image: radial-gradient(circle at top left, transparent 70.5%, #39687f 100%);
				z-index: -1;
			}
			&--open {
				position: fixed;
				top: 0;
				left: 0;
				right: 0;
				bottom: 0;
				&::before {
					background-image: radial-gradient(circle at top left, transparent 70.5%, rgba(#ca2c92, 0.5) 100%);
				}
			}
		}
		@include media('>desktop') {
			order: 1;
			position: sticky;
			top: calc((100vh - 675px) / 2);
			background-position: 0 50%;
			&::before {
				display: block;
				pointer-events: none;
				content: '';
				position: absolute;
				top: 0;
				left: 0;
				width: 50%;
				height: 675px;
				transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
				background-image: linear-gradient(to left, #000, transparent), url('~@/static/me.jpg?resize&size=600&format=webp');
				background-size: cover;
				background-position: top right;
				@include media('retina2x') {
					background-image: linear-gradient(to left, #000, transparent), url('~@/static/me.jpg?resize&size=1200&format=webp');
				}
				z-index: -1;
				border-radius: 40px 0 0 40px;
			}
		}
	}
	&__links {
		list-style-type: none;
		padding: 0;
		@include media('<desktop') {
			position: fixed;
			left: 100%;
			top: 50%;
			text-transform: uppercase;
			text-align: right;
			transform: translateY(-50%);
			li {
				margin: 5px 0;
				transform: translatex(0);
				transition: all 0.35s cubic-bezier(0.16, 1, 0.3, 1);
				transition-delay: calc((var(--children) - var(--child-n)) * 0.05s);
			}
			&--open {
				li {
					transform: translatex(-100%);
					transition-delay: calc(var(--child-n) * 0.05s);
				}
			}
		}
		@include media('>desktop') {
			display: flex;
			justify-content: space-around;
			overflow: hidden;
			background-image: linear-gradient(to bottom, $shark 50px, transparent 50px);
			background-repeat: no-repeat;
			&::before {
				display: block;
				pointer-events: none;
				content: '';
				position: absolute;
				top: 0;
				left: 0;
				right: 0;
				height: 100px;
				background-image: linear-gradient(to bottom, #000 50px, transparent);
				border-radius: 40px 40px 0 0;
			}
			li {
				transform: none;
			}
		}
		#{$a-tags} {
			color: #fff;
			font-family: 'Nunito';
			display: inline-block;
			font-size: 24px;
			line-height: 30px;
			transform: translateY(-4px);
			padding: 6px 50px 4px 15px;
			margin-bottom: 10px;
			text-decoration: none;
			transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
			letter-spacing: 1px;
			text-rendering: optimizeLegibility;
			position: relative;
			@include media('>desktop') {
				padding: 15px 20px 20px 20px;
				margin: 0;
				font-size: 20px;
				text-transform: uppercase;
				transform: none;
			}
			&::before,
			&::after {
				display: block;
				content: '';
				position: absolute;
				top: 50%;
				right: 20px;
				transform-origin: center;
				background: rgba(255, 255, 255, 0.5);
				width: 20px;
				height: 5px;
				border-radius: 10px;
				transform: translatey(-50%);
				transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
				@include media('>desktop') {
					top: auto;
					bottom: 5px;
					right: auto;
					left: 50%;
					transform: translatex(-50%) scale(0.75);
				}
			}
			&::before {
				transform: translatey(-50%) rotate(90deg);
				@include media('>desktop') {
					transform: translatex(-50%) rotate(90deg) scale(0.75);
				}
			}
		}
		#{$a-tags-hover} {
			color: #ca2c92;
			&::before,
			&::after {
				background: rgba(#ca2c92, 0.5);
			}
			&::before {
				transform: translatey(-50%) rotate(135deg) scale(1.2);
			}
			&::after {
				transform: translatey(-50%) rotate(45deg) scale(1.2);
			}
			@include media('>desktop') {
				&::before {
					transform: translatex(-50%) rotate(135deg) scale(1);
				}
				&::after {
					transform: translatex(-50%) rotate(45deg) scale(1);
				}
			}
		}
		@include media('<desktop') {
			#{$a-tags-hover} {
				letter-spacing: 2px;
			}
		}
	}
	&__hamburger {
		display: none;
		@include media('<desktop') {
			display: block;
			outline: 0;
			position: fixed;
			border: 0;
			background: #fff;
			width: 40px;
			height: 40px;
			border-radius: 100%;
			bottom: 15px;
			right: 15px;
			z-index: 0;
			&::before,
			&::after {
				display: block;
				content: '';
				position: absolute;
				left: 50%;
				transform-origin: center;
				background: transparent;
				width: 20px;
				height: 9px;
				transform: translate(-50%, calc(-50% + 3px));
				transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
				border-top: 3px solid #38667e;
				border-bottom: 3px solid #38667e;
			}
			&::before {
				transform: translate(-50%, calc(-50% - 3px));
			}
			&--open {
				&::before,
				&::after {
					background: rgba(#ca2c92, 0.5);
					border-radius: 10px;
					border-color: transparent;
					height: 5px;
				}
				&::before {
					transform: translate(-50%, -50%) rotate(135deg) scale(1.2);
				}
				&::after {
					transform: translate(-50%, -50%) rotate(45deg) scale(1.2);
				}
			}
		}
	}
}
</style>
