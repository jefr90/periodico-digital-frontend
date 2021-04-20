<template >
  <div class="max-w-xl mx-auto">
    <h1 class="text-lg font-semibold mt-4">Lista de Noticias</h1>
    <NewsListItem
      v-for="newsItem in news"
      v-bind:key="JSON.parse(newsItem.content)._id"
      :newsItem="newsItem"
    >
    </NewsListItem>
  </div>
</template>

<script>
import NewsListItem from "../components/NewsListItem";
export default {
  name: "NewsList",
  components: { NewsListItem },
  props: ["news"],
};
</script>