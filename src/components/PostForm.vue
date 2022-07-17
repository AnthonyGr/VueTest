<template>
    <form @submit.prevent>
        <h4>Создать пост</h4>
        <input
          class="input"
          type="text"
          placeholder="Название"
          v-model="post.title"
        />
        <input
          class="input"
          type="text"
          placeholder="Описание"
          v-model="post.body"
        />
        <Button @click="createPost">Создать</Button>
    </form>
</template>

<script>
import Button from "./UI/Button";

export default {
    components: {Button},
    data() {
        return {
            post: {
                title: "",
                body: "",
            },
        };
    },
    methods: {
        createPost() {
            this.post.id = Date.now();
            this.$emit("create", this.post);
            this.post = {
                title: "",
                body: "",
            };
        },
    },
};
</script>

<style lang="sass">
.input
    box-sizing: border-box
    width: 100%
    padding: 10px 15px
    margin-bottom: 15px
    border: 1px solid teal
</style>
