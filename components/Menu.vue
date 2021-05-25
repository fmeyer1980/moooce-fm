<template>
    <nav id="menu-element" class="main-nav [] [ bg-primary-shade color-light-glare pt-900 lg:pt-xl ]">
		<div class="main-nav__inner-wrapper [ container-narrow ] []">
			<PriceItem product-id="d4f80ab7-3d65-43f6-901e-a5e786a6211a" />
			<ul class="pt-600 text-200">
				<li v-for="item in site.mainMenu" :key="item._key">
					<nuxt-link :to="{name:'slug',params:{slug:item.slug.current}}" title="Handelsbetingelser">{{ item.name }}</nuxt-link>
				</li>
			</ul>
		</div>
    </nav>
</template>

<script>
	import {mapState} from "vuex";
	import PriceItem from "@/components/PriceItem";
	export default {
		name: "Menu",
		components: {PriceItem},
		computed: {
            ...mapState('sanity',{
				site: 'siteSettings'
			}),
			...mapState('view', {
				menuOpen: 'menuOpen'
			})
		},
		watch:{
			'$route'(to){
				if(this.menuOpen)
					this.$store.commit('view/setMenuOpen',false);
			}
		}
	};
</script>

<style lang="scss">
@import './assets/scss/config';
$outputTokenCSS: false;
@import './node_modules/gorko/gorko.scss';

.main-nav{
	position: fixed;
	top: 0;
	z-index: 50;
	width: 100%;
	height: 100%;
	min-height: 100vh;
	transition: transform 300ms ease-in-out;
	transform: translateY(-100%);
	overflow-y: scroll;

	&::before{
		content: "";
		background-image: url('https://cdn.sanity.io/images/vn5aapzu/production/c10c17f387540ceaf6b4afabd69f2bf5291445d3-1800x1257.jpg?w=1200&q=50&auto=format');
		background-size: cover;
		position: absolute;
		top: 0px;
		right: 0px;
		bottom: 0px;
		left: 0px;
		opacity: 0.3;
	}
	
	.open & {
		transform: translateY(0%);
	}

	&__inner-wrapper{
		position: relative;
		display: grid;
		grid-template-columns: 1fr;
		
		@include media-query('md'){
			grid-template-columns: 20rem 1fr;
			gap: get-size('900');
		}

		ul{
			display: flex;
			flex-wrap: wrap;
			align-self: start;

			li{
				flex-basis: 100%;

				@include media-query('lg'){
					flex-basis: 50%;
				}

				a{
					opacity: .8;
					padding: .4em;
					display: inline-block;
				}
			}
		}

		> div{
			display: none;

			@include media-query('md'){
				display: block;
			}
		}
	}

	&__bg-image{
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		object-fit: cover;
		object-position: top center;
		opacity: 0.3;
		z-index: -1;
	}


}

</style>