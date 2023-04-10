<template>
  <form @submit.prevent>
    <h4>Создание поста</h4>
    <!-- v-model ДВУСТОРОННЕЕ СВЯЗЫВАНИЕ (ВМЕСТО СОБЫТИЯ ONINPUT(ИЛИ ONCHANGE И ТД) И VALUE) -->
    <my-input v-model="post.title" v-model:value="post.title" type="text" placeholder="Название" />
    <my-input v-model="post.body" type="text" placeholder="Описание" />
    <my-button class="btn" @click="createPost">Создать!</my-button>
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
    createPost(e) {
      this.post.id = new Date();
      // ПЕРЕДАЧА ИНФЫ В РОДИТЕЛЯ
      //   СОБЫТИЕ ДЛЯ СЛУШАНИЯ И ДАННЫЕ
      this.$emit("create", this.post, `uha!!!`);

      this.post = {
        title: "",
        body: "",
      };
    },
  },
  watch: {
    post: {
      handler(newVal) {
        console.log(newVal);
      },
      deep: true
    }
  }
};
</script>

<style>
form {
  display: flex;
  flex-direction: column;
}

.btn {
  align-self: flex-end;
}
</style>
