<template>
  <div class="post">
    <div>
      <div><strong>Название:</strong> {{ post.title }}</div>
      <div><strong>Описание:</strong> {{ post.body }}</div>
    </div>
    <div class="post__btns">
      <Button @click="$emit('remove', post)">Удалить</Button>
    </div>
  </div>
</template>
<script>
import Button from "./UI/Button";

export default {
  components: { Button },
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style lang="sass">
.post
    margin-top: 15px
    padding: 15px
    border: 2px solid #336699
    border-radius: 10px
    display: flex
    align-items: center
    justify-content: space-between
</style>
