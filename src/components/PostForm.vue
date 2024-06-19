<template>
  <form class="form-post" @submit.prevent>
    <h4>Создание поста</h4>
    <input
      v-model="post.title"
      class="form-post__input"
      type="text"
      placeholder="Название"
    />
    <input
      v-model="post.body"
      class="form-post__input"
      type="text"
      placeholder="Описание"
    />
    <my-button class="form-post__btn" @click="createPost">Создать</my-button>
  </form>
</template>

<script>
import MyButton from "@/components/UI/MyButton";
export default {
  components: { MyButton },
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
      if (this.post.title && this.post.body) {
        this.post.id = Date.now();
        this.$emit("create", this.post);
        this.post = {
          title: "",
          body: "",
        };
      }
    },
  },
};
</script>

<style scoped>
.form-post {
  display: flex;
  flex-direction: column;
}
.form-post__input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}
.form-post__btn {
  align-self: flex-end;
  margin-top: 15px;
  color: #fff;
  background: teal;
}
</style>