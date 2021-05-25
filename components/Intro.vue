<template>
    <div class="intro">
        <div class="intro__mobil-media">
            <div class="lines"></div>
            <div class="video-wrapper">
                <img src="/images/iphone-x.webp" alt="Iphone cover"/>
                <video class="video-bg" muted loop autoplay playsinline>
                    <source :src="home.intro.video" type="video/mp4">
                    <source :src="home.intro.video" type="video/webm">
                    Your browser does not support the video tag.
                </video>
            </div>
        </div>
        <div class="intro__content [] [ bg-primary color-light-glare ]">
            <div class="intro__content__inner-wrapper [ flow ] [ space-200 pr-gutter ]">
                <h1 class="[] [ text-500 ]" v-text="home.intro.headline" />
                <p class="[] [ text-300 ]" v-text="home.intro.subHeadline" />
                <SanityContent class="page-content flow measure-short" :blocks="home.intro.text" />
            </div>
        </div>
        <div class="intro__mobil-product [] [ color-light-glare ]">
            <div class="[] [ pr-700 ]">
                <img loading="lazy" v-if="home.intro.productImage.asset" 
                :srcset="$urlFor(home.intro.productImage).width(400).auto('format').quality('70') + ' 1x, ' + $urlFor(home.intro.productImage).width(800).auto('format').quality('70') + ' 2x'" :alt="home.intro.productImage.alt" />
                <ArrowCurveSvg class="border-arrow [ fill-current h-600 ]" />
            </div>
            <div class="intro__mobil-product__bottom [ flow ] [ space-300 ]">
                <ArrowDownSvg class="[] [ fill-current h-400 ]" />
                <p class="[] [ text-200 weight-black measure-micro-xxs ]">Sælg direkte via dine videoer</p>
                <ArrowDownSvg class="[] [ fill-current h-400 ]" />
            </div>
        </div>
    </div>
</template>

<script>
    import { SanityContent } from '@nuxtjs/sanity/dist/components/sanity-content'
    import ArrowCurveSvg from '@/components/svg/ArrowCurveSvg'
    import ArrowDownSvg from '@/components/svg/ArrowDownSvg'
    
    import {ScrollTrigger} from 'gsap/ScrollTrigger'

	export default {
		name: "Intro",
        components: {SanityContent,ArrowCurveSvg,ArrowDownSvg},
        props:{
            home: Object
        },
        mounted()
		{
			if(process.client)
			{
				if(document.querySelectorAll('.header-animation-trigger').length > 0)
				{
					if (window.innerWidth > 992)
					{
						this.$gsap.registerPlugin(ScrollTrigger)
						var options = {
							scrollTrigger: {
								trigger: ".header-animation-trigger",
								pin: ".header-animation-trigger",
								scrub: true,
								markers: false
							}
						}
						let tl = this.$gsap.timeline(options);
						tl.to(".video-wrapper", {
							top: 35,
							ease: 'sine.inOut'
						});
 					    tl.to(".intro__mobil-product__bottom", {
							top: 300,
							opacity: 1,
							ease: 'sine.inOut'
						}, 0);
					}
				}
			}
		}
	};
</script>

<style lang="scss" scoped>
@import './assets/scss/config';

$outputTokenCSS: false;
@import './node_modules/gorko/gorko.scss';


.intro{
    --mobil-vide-size: calc(var(--size-xl) * 3.2);

    position: relative;

    @include media-query('lg'){
        padding-left: calc(((100% - var(--container-width)) / 2) - var(--gutter));
        padding-right: calc(((100% - var(--container-width)) / 2) - var(--gutter));
        border-left: var(--gutter) solid transparent;
        border-right: var(--gutter) solid transparent;
    }

    
    &__mobil-media{
        position: relative;
        height: calc( var(--mobil-vide-size) - calc(var(--size-lg) * 2) + var(--size-400));
        background-color: get-color('primary');

        @include media-query('lg'){
            position: static;
            background-color: transparent;
            height: auto;
            margin-top: -20rem;
        }

        .lines{
            position: absolute;
            bottom: 0;
            right: calc(var(--gutter) * 2);
            border: 1px solid #fff;
            height: calc( var(--mobil-vide-size) - calc(var(--size-lg) * 2));
            width: calc(100% - calc(var(--size-400) * 3));
            border-radius: 27px 0 0 27px;
            border-right: 0;

            @include media-query('lg'){
                display: none;
            }

            &::after{
                content: "";
                position: absolute;
                bottom: calc(-1 * var(--gutter));
                right: calc(-1 * var(--gutter));
                width: get-size('gutter');
                height: get-size('gutter');
                border-top: 1px solid #fff;
                border-right: 1px solid #fff;
                border-top-right-radius: 27px;
                
            }
        }

        .video-wrapper{
            position: absolute;
            top: calc(-1 * var(--size-lg) * 2);
            right: get-size('gutter');
            height: var(--mobil-vide-size);
            box-shadow: 10px 10px 31px 0px rgba(0,0,0,0.75);
            -webkit-box-shadow: 10px 10px 31px 0px rgba(0,0,0,0.75);
            -moz-box-shadow: 10px 10px 31px 0px rgba(0,0,0,0.75);
            border-radius: 15%;
            z-index: 40;

             img{
                height: 100%;
            }

            video{
                position: absolute;
                top: 1px;
                left: 1px;
                z-index: -1;
                width: 99%;
                height: 99%;
                border-radius: 18%;
            }
        }
    }

    &__content{
        padding: get-size('gutter');

        @include media-query('lg'){
            padding: get-size('700') 0 calc(var(--size-lg) + var(--size-600)) get-size('600');
            margin-right: var(--size-xl);
        }

        &__inner-wrapper{
            border-right: 1px solid #fff;

            @include media-query('lg'){
                border: none;
                max-width: 70%;
            }
        }
        
    }

    &__mobil-product{
        position: relative;
        background-color: get-color('primary');
        padding-bottom: get-size('300');

        @include media-query('lg'){
            position: absolute;
            top: 0;
            right: 0;
            width: 30rem;
            background-color: transparent;
            padding-bottom: 0;
            opacity: 0;
            z-index: 99;
        }

        .border-arrow{
            position: absolute;
            top: calc(-1 * calc(var(--gutter) + 1px));
            right: calc(var(--gutter) - .5px);
        }

        &__bottom{
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
        }
    }
}
</style>