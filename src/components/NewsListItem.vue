<template>
    <h1>News List Item</h1>
    <div class="border: 1px solid black">
        <h2 class="row">
            {{this.content.title}}
        </h2>
        <h2 class="row">
            {{this.content.description}}
        </h2>
        <h2 class="row">
            {{this.content.author}}
        </h2>
        <h2 class="row">
            {{this.content.createdAt}}
        </h2>
    </div>
</template>

<script>

export default {
    name: "NewsListItem",
    components: {},
    data () {
        return {content: {}}
    },
    props: ['newsItem'],
    created(){
        this.content = JSON.parse(this.newsItem.content)
        console.log(this.content)
    }
}
</script>