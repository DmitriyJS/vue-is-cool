<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <div class="app__btns">
      <my-button @click="showDialog">Создать пост</my-button>
      <my-select :options="sortOptions" v-model="selectedSort"></my-select>
    </div>
    <my-dialog v-model:show="dialogVisible">
      <post-form @create="createPost"></post-form>
    </my-dialog>
    <post-list v-if="!isPostsLoading" :posts="posts" @remove="removePost"></post-list>
    <div v-else>идет загрузка...</div>
  </div>
</template>

<script>
import PostList from "@/components/PostList.vue";
import PostForm from "@/components/PostForm.vue";
import axios from "axios";

export default {
  components: { PostList, PostForm, },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      modificatorValue: "",
      isPostsLoading: true,
      selectedSort: "",
      sortOptions: [
        { value: "title", body: "По названию" },
        { value: "body", body: "По описанию" },
      ]
    };
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter(item => item.id != post.id)
      console.log(post)
    },
    showDialog() {
      this.dialogVisible = true
    },
    async fetchPosts() {
      try {
        this.isPostsLoading = true;
        setTimeout(async () => {
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
          this.posts = response.data;
          this.isPostsLoading = false;
          console.log(response);
        }, 1000)

      } catch (error) {
        alert(error)
      }
      // https://jsonplaceholder.typicode.com/posts?_limit=10
    }
  },
  mounted() {
    this.fetchPosts();
  },
  watch: {
      // selectedSort(newValue, old){
      //  this.posts.filter(post => )
      // }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  border: none;
}

.app {
  padding: 20px;
}

.app__btns {
  display: flex;
  justify-content: space-between;
  margin: 15px;
}
</style>
