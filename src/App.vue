<template>
  <div class="app">
    <div class="app__buttons">      
      <my-button class="app__post-btn" @click="showDialog">Создать пост</my-button>
      <my-select 
        v-model="selectedSort"
        :options="sortOptions"
      />
    </div>    
    <my-dialog v-model:show="dialogVisible">
      <post-form @create="createPost"/>
    </my-dialog>    
    <post-list 
      @remove="removePost"
      :posts="sortedPosts"
      v-if="!isPostsLoading"
    />
    <div v-else>Идёт загрузка...</div>
    
  </div>
</template>

<script>
import PostForm from '@/components/PostForm'
import PostList from '@/components/PostList'
import axios from 'axios';
export default {
  components: {
    PostList, PostForm
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostsLoading: false,
      selectedSort: '',
      sortOptions: [
        {value: 'title', name: 'По названию'},
        {value: 'body', name: 'По содержимому'}
      ]
    };
  },
  methods: {
    createPost(post) {
      this.posts.push(post)
      this.dialogVisible = false
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id) // перезаписываем массив: фильтруем массив по посту, который удаляем
    },
    showDialog() {
      this.dialogVisible = true
    },
    async fetchPosts() {
      try {
        this.isPostsLoading = true
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
        this.posts = response.data
      } catch(e) {
        alert('Ошибка!')
      } finally {
        this.isPostsLoading = false
      }
    }
  },
  mounted() {
    this.fetchPosts()
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((post1, post2)=> post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
    }
  },
  watch: {
    // selectedSort(newValue) { // Эта функция сразу является хэндлером, т.к. это простой тип данных и функцию handler() и свойство deep: true мы не используем внутри объекта selectedSort
    //   this.posts.sort((post1, post2)=> {
    //     return post1[newValue]?.localeCompare(post2[newValue])
    //   })
    // },
    // dialogVisible(newValue) {
    //   console.log(newValue)
    // },
    // isPostsLoading(newValue) {
    //   console.log(newValue)
    // }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.app {
  padding: 20px;
}
.app__buttons {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 15px;
}
</style>
