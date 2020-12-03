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
					to: '/about'
				},
				{
					title: 'Experience',
					to: '/experience'
				},
				{
					title: 'Endorsements',
					to: '/endorsements'
				},
				{
					title: 'Contact',
					to: '/contact'
				},
				{
					title: 'Game',
					to: '/game'
				}
			]
		};
	}
};
</script>

<style lang="scss">
@import '@/assets/mixins.scss';
.nav {
	&__container {
		&::before {
			display: block;
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
	&__links {
		position: fixed;
		padding: 0;
		list-style-type: none;
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
			}
			&::before {
				transform: translatey(-50%) rotate(90deg);
			}
		}
		#{$a-tags-hover} {
			letter-spacing: 2px;
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
		}
	}
	&__hamburger {
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
</style>
