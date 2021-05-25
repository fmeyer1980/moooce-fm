<template>
    <section class="page-header [ container-narrow flow ] [ pt-lg pb-600 space-xs ]">
        <h1 class="[] [ measure-micro ]" v-text="(pages.headline) ? pages.headline : pages.name" />
        <p class="[] [ text-300 measure-compact leading-tight ]" v-if="pages.summary" v-text="pages.summary" />
    </section>
    <!-- <div class="page-header [ container-narrow flow ] [ pt-xl pb-600 space-xs ]">
        <h1 class="[] [ measure-micro ]" v-text="headline" />
        <p class="[] [ text-300 measure-compact leading-tight ]" v-if="summary" v-text="summary" />
    </div> -->
</template>

<script>
	export default {
		name: "PageHeader",
        props:{
            pages: Object
        }
    }

    // export default {
	// 	name: "PageHeader",
    //     props:{
    //         headline: String,
    //         summary: String
    //     }
    // }
</script>

<style lang="scss" scoped>
    .page-header{
        border-bottom: 1px solid rgba(#000, .05);
    }
</style>
