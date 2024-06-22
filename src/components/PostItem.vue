<template>
  <div class="post">
    <div>
      <div><strong>Id:</strong> {{ post.id }}</div>
      <div><strong>Название:</strong> {{ post.title }}</div>
      <div><strong>Описание:</strong> {{ post.body }}</div>
    </div>
    <div class="post__btns">
      <my-button
        @click="$emit('remove', post)"
        class="post__remove">Удалить</my-button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
.post {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.post__remove {
  padding: 2px 6px !important;
}
</style>
