<template>
  <div>
    <Header />

    <div class="container">
      <div class="grid">
        <NuxtLink class="grid_item" :to="'/post/' + item.id" style="font-size: 15rem;" v-for="(item, index) in posts"
          :key="index">
          <div class="title">{{ item.title }}</div>
          <div class="content">{{ getContent(item.content) }}</div>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
import Header from '../components/Header.vue';

export default {
  name: 'IndexPage',
  data() {
    return {
      posts: []
    }
  },
  methods: {
    async getPosts() {
      this.posts = await this.$axios.$get('/data/posts.json');
    },

    getContent(text) {
      if (text.length >= 25) {
        return text.substring(0, 25) + '...'
      }
      return text
    }
  },
  mounted() {
    this.getPosts();
  }
}
</script>

<style lang="scss" scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 30rem;

  &_item {
    text-decoration: none;
    color: black;
    background-color: white;
    box-shadow: rgba(100, 100, 111, 0.108) 0px 3px 19px 0px;
    padding: 10rem 17rem;
    font-weight: 500;
  }

  .content {
    margin-top: 10rem;
    color: gray;
    font-size: 14rem;
  }

  .title {
    font-size: 17rem;
  }
}
</style>
