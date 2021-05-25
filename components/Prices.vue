<template>
	<section class="prices" id="getstarted">
        <div class="prices__image-wrapper">
            <!-- <img :src="$urlFor(home.featuredProducts.bgImage).width(1800).auto('format').quality('70')" :alt="home.featuredProducts.bgImage.alt" loading="lazy" /> -->

            <!-- <img class="[ w-full ]" 
                loading="lazy" 
                :srcset="$urlFor(home.featuredProducts.bgImage).width(900).auto('format').quality('70') + ' 1x,' + $urlFor(home.featuredProducts.bgImage).width(1800).auto('format').quality('70') + ' 2x'" 
                :alt="home.featuredProducts.bgImage.alt"> -->



            <img width="480" height="315" loading="lazy"
                :src="$urlFor(home.featuredProducts.bgImage).width(480).height(315).auto('format').quality('70')" 
                :srcset="
                $urlFor(home.featuredProducts.bgImage).width(480).height(315).auto('format').quality('30') + ' 480w, ' +
                $urlFor(home.featuredProducts.bgImage).width(768).height(504).auto('format').quality('30') + ' 768w, ' +
                $urlFor(home.featuredProducts.bgImage).width(1024).height(672).auto('format').quality('70') + ' 1024w, ' +
                $urlFor(home.featuredProducts.bgImage).width(1280).height(840).auto('format').quality('70') + ' 1280w, ' +
                $urlFor(home.featuredProducts.bgImage).width(1600).height(1050).auto('format').quality('70') + ' 1600w, '
                " 
                :alt="home.featuredProducts.bgImage.alt"
            />
        </div>
		<div class="prices__list [ container-narrow ]">
			<PriceItem v-for="product in home.featuredProducts.products" :key="product._id" :product-id="product._id" />
		</div>
	</section>
</template>
<script>
	import PriceItem from "@/components/PriceItem";
	export default {
		name: "Prices",
        components: {PriceItem},
		props:{
            home: Object
        }
	};
</script>
<style lang="scss" scoped>
    @import './assets/scss/config';

    $outputTokenCSS: false;
    @import './node_modules/gorko/gorko.scss';

    .prices{
        position: relative;
        margin-top: calc(-1 * var(--size-600));
        padding: 0 0 var(--size-400);

        @include media-query('md'){
            margin-top: 0;
            padding: calc(var(--size-lg) * 1.2) 0 var(--size-lg);
        }

        &__image-wrapper{

            img{
                position: absolute;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                object-fit: cover;
                object-position: center top;
            }


            &::before{
                content: "";
                position: absolute;
                top: 0;
                left: 0;
                width: 100%;
                height: 8rem;
                background: linear-gradient(to bottom, rgba(get-color('light-shade'), 1), transparent);
                z-index: 1;
            }
        }

        &__list{
            position: relative;
            display: grid;
            grid-template-columns: 1fr;
            gap: get-size('gutter');
            z-index: 10;

            @include media-query('md'){
                grid-template-columns: repeat(3, 1fr);
                align-items: center;
            }
        }
    }
</style>