<template>
<div>
    <PageHeader v-if="!pages.hidePageHeader" :pages="pages" />
    <component v-for="item in pages.pageModules" :key="item._id" :is="componentMap[item._type]" :item="item" />
</div>
</template>

<script>
import {mapState} from 'vuex'
import { groq } from '@nuxtjs/sanity'

import PageHeader from '@/components/PageHeader'
import BodyText from '@/components/pageModules/BodyText'
import HowToUse from '@/components/pageModules/HowToUse'
import Intro from '@/components/pageModules/Intro'
import PriceList from '@/components/pageModules/PriceList'
import CoverImage from '@/components/pageModules/CoverImage'


export default {
    async asyncData({ params, $sanity }) {
        const query = groq`*[_type == "pages" && slug.current == "${params.slug}"]{
            meta{
                title,
                description
            },
            name,
            slug,
            headline,
            summary,
            showSitebar,
            hidePageHeader,
            pageModules[]{
                _key,
                products[]->,
                ...,
            }
        }[0]`
        const pages = await $sanity.fetch(query)
        return { pages }
    },
    components: {PageHeader},
    computed:{
        ...mapState('sanity',{
            site: 'siteSettings'
        })
    },
    data(){
        return {
            componentMap: {
                bodyText: BodyText,
                howToUse: HowToUse,
                intro: Intro,
                priceList: PriceList,
                coverImage: CoverImage
            },
        }
    },
}
</script>
