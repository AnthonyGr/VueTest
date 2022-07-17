<template>
    <div class="wrapper">
        <PostForm @create="createPost"/>
        <PostList :posts="posts" @remove="removePost"/>
    </div>
</template>

<script>
import PostForm from "./components/PostForm";
import PostList from "./components/PostList";

export default {
    components: {PostForm, PostList},
    data() {
        return {
            posts: [
                {id: 1, title: "JavaScript", body: "Описание 1"},
                {id: 2, title: "JavaScript", body: "Описание 2"},
                {id: 3, title: "Vue", body: "Описание 3"},
            ],
        };
    },
    methods: {
        createPost(post) {
            this.posts.push(post);
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id);
        }
    },
};
</script>

<style lang="sass" scoped>
*
    margin: 0
    padding: 0
    box-sizing: border-box

.wrapper
    max-width: 800px
    padding: 30px 20px
    margin: 0 auto
</style>
