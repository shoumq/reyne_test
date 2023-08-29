<template>
    <div>
        <Header />

        <div class="container post">
            <div class="title">{{ result.title }}</div>
            <div class="content">{{ result.content }}</div>
        </div>
    </div>
</template>

<script>
import Header from '~/components/Header.vue';

export default {
    name: 'PostPage',
    data() {
        return {
            posts: [],
            result: {},
            id_param: parseInt(this.$route.params.id)
        }
    },
    methods: {
        async getPostById() {
            this.posts = await this.$axios.$get('/data/posts.json');
            this.result = this.posts.find(x => x.id === this.id_param);
            if (this.result === undefined) {
                this.$nuxt.$router.replace({ path: '/'});
            }
        }
    },
    mounted() {
        this.getPostById();
    }
}
</script>


<style lang="scss" scoped>
.post {
    .title {
        font-size: 20rem;
        margin-bottom: 10rem;
    }
    .content {
        font-size: 17rem;
        color: rgb(86, 86, 86);
    }
}
</style>
