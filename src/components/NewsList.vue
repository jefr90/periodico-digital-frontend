<template>
    <h1>News List</h1>
    <NewsListItem v-for="newsItem in news" v-bind:key="newsItem._id" :newsItem="newsItem">
    </NewsListItem>
</template>

<script>

import NewsListItem from '../components/NewsListItem'
export default {
    name: "NewsList",
    components: {NewsListItem},
    props: ['news']
}
</script>