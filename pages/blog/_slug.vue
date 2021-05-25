<template>
    <div class="post">
        <PostBanner 
            :name="post.name" 
            :headline="post.headline" 
            :summary="post.summary" 
            :image="post.mainImage"
            :imageDarkness="post.darkImage"
        />
        <div class="[ container-narrow pt-600 pb-600 ]">
             <SanityBlocks className="page-content [ flow ] [ space-base-em ]"  v-if="post.body" :blocks="post.body" :serializers="serializers" />
        </div>
        <div class="post__featuredPosts [ container-narrow flow ] [ bg-light-shade-dark pt-800 pb-800 space-600 ]" >
            <PostCard class="post__featuredPosts__item" v-for="item in post.featuredPosts" :key="item._id" :item="item" />
        </div>
    </div>
</template>

<script>
    import { groq } from '@nuxtjs/sanity'
    import PostCard from "@/components/PostCard";
    import SanityBlocks from 'sanity-blocks-vue-component';
    import ContentImage from '@/components/ContentImage'

export default {
    async asyncData({ params, $sanity }) {
        const query = groq`*[_type == "post" && slug.current == "${params.slug}"]{
            meta{
                title,
                description
            },
            name,
            slug,
            headline,
            summary,
            mainImage,
            body[] {
                ...,
                asset->,
                children[] {
                    ...,
                }
            },
            darkImage,
            featuredPosts[]->{
                name,
                slug,
                headline,
                summary,
                mainImage
            }
        }[0]`
        const post = await $sanity.fetch(query);
        return { post }
    },
    components: {SanityBlocks,PostCard},
     data() {
        return {
            serializers: {
                types: {
                    image: ContentImage,
                }
            }
        }
    },
    head() {
        return {
            title: this.post.meta.title,
            meta: [
                {
                    hid: 'description',
                    name: "description", 
                    content: this.post.meta.title
                }
            ]
        }
    },
    meta: {
		pageClasses: ['moooce-prices'],
	},
}
</script>
<style lang="scss">
@import './assets/scss/config';

$outputTokenCSS: false;
@import './node_modules/gorko/gorko.scss';

.post{

    &__featuredPosts{

        // &__item{
        //     display: grid;
        //     grid-template-columns: 1fr;
        //     gap: get-size('400');

        //     @include media-query('md'){
        //         grid-template-columns: 1fr 1fr;
        //         gap: 0;

        //         &:nth-child(even){
                    
        //             .image-wrapper{
        //                 order: 2;
        //             }

        //             .content{
        //                 order: 1;
        //             }
        //         }
        //     }
        // }
    }
}
</style>
