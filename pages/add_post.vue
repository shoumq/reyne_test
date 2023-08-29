<template>
    <div>
        <Header />
        <div class="container">
            <div class="title">Добавить статью</div>

            <form class="form" @submit.prevent="createPost">
                <label for="title">
                    Название
                    <input type="text" id="title" v-model="title">
                </label>

                <label for="title">
                    Контент
                    <input type="text" id="title" v-model="content">
                </label>

                <button class="btn">Добавить</button>
            </form>
        </div>
    </div>
</template>


<script>
import Header from '../components/Header.vue';

export default {
    name: 'AddPostPage',
    data() {
        return {
            title: null,
            content: null,
            posts: []
        }
    },
    methods: {
        async createPost() {
            this.posts = await this.$axios.get('/data/posts.json');
            console.log(this.posts);
        }
    }
}
</script>


<style lang="scss" scoped>
.title {
    font-size: 25rem;
    margin-bottom: 20rem;
    font-weight: 500;
}
</style>
