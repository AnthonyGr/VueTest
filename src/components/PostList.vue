<template>
    <div v-if="posts.length > 0">
        <h3>Список постов:</h3>
        <PostItem
          v-for="post in posts"
          :post="post"
          :key="post.id"
          @remove="$emit('remove', post)"
        />
    </div>
    <h3 v-else>Постов нет</h3>
</template>

<script>
import PostItem from "./PostItem";

export default {
    components: {PostItem},
    props: {
        posts: Array,
    },
    data() {
        return {};
    },
};
</script>

<style lang="sass"></style>
