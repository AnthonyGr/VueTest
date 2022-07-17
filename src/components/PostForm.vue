<template>
    <form @submit.prevent>
        <h4>Создать пост</h4>
       <MyInput v-model="post.title" placeholder="Название"/>
       <MyInput v-model="post.body" placeholder="Текст"/>
        <Button @click="createPost">Создать</Button>
    </form>
</template>

<script>
import Button from "./UI/Button";
import MyInput from "@/components/UI/MyInput";

export default {
    components: {MyInput, Button},
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

</style>
