<template>
  <transition name="fade" mode="out-in">
    <div class="rounded shadow-lg m-5">
      <h1
        v-bind:style="{ backgroundColor: this.content.topic.color }"
        class="rounded font-bold"
      >
        {{ this.content.topic.description }}
      </h1>
      <div class="p-2 border-gray-200 rounded border-8">
        <p class="row font-semibold flex p-1">
          {{ this.content.title }}
        </p>
        <h2 class="row">
          {{ this.content.description }}
        </h2>
        <h2 class="row text-gray-500 flex py-2">
          Escrito por {{ this.content.authorName }} el {{ publicationDate }} a
          las
          {{ publicationTime }}
        </h2>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "NewsListItem",
  components: {},
  data() {
    return { content: {}, topic: {} };
  },
  props: ["newsItem"],
  created() {
    this.content = JSON.parse(this.newsItem.content);
  },
  computed: {
    publicationDate() {
      let date = new Date(this.content.createdAt);
      return (
        date.getDate() + "/" + (date.getMonth() + 1) + "/" + date.getFullYear()
      );
    },
    publicationTime() {
      let date = new Date(this.content.createdAt);
      return date.getHours() + ":" + this.addZero(date.getMinutes());
    },
  },
  methods: {
    addZero: (i) => {
      if (i < 10) {
        i = "0" + i;
      }
      return i;
    },
  },
};
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.35s ease;
}

.fade-enter-from,
.fade-leave-active {
  opacity: 0;
}
</style>