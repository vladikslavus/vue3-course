<template>
  <form class="form-post" @submit.prevent>
    <h4>Создание поста</h4>
    <my-input
      v-model.trim="post.title"
      type="text"
      placeholder="Название"
    />
    <my-input
      v-model.trim="post.body"
      type="text"
      placeholder="Описание"
    />
    <my-button class="form-post__btn" @click="createPost">Создать</my-button>
  </form>
</template>

<script>
export default {
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
  watch: {
    post: {
      handler(newVal) {         // Т.к. это объект, то используем функцию handler()
        console.log(newVal)
      },
      deep: true                // и используем "Глубокое отслеживание"
    }
  }
};
</script>

<style scoped>
.form-post {
  display: flex;
  flex-direction: column;
}
.form-post__btn {
  align-self: flex-end;
  margin-top: 15px;  
  color: #fff !important;
  background: teal !important;
}
</style>