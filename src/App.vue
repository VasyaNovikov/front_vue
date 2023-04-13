<template>
  <div class="app">
    <form @submit.prevent>
      <h4>Creating a post</h4>
      <input
        v-bind:value="title"
        @input="title = $event.target.value"
        class="input" type="text"
        placeholder="post title"
      >
      <input
        v-bind:value="body"
        @input="body = $event.target.value"
        class="input" type="text"
        placeholder="post description"
      >
      <button class="btn" @click="createPost">Create</button>
    </form>
    <div class="post" v-for="post in posts">
      <div><strong>post title: </strong>{{ post.title }}</div>
      <div><strong>post description: </strong>{{ post.body }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: [
             {id: 1, title: 'javascript1', body: 'post description1'},
             {id: 2, title: 'javascript2', body: 'post description2'},
             {id: 3, title: 'javascript3', body: 'post description3'}
             ],
             title: '',
             body: '',
    }
  },
  methods: {
    createPost() {
      const newPost = {
        id: Date.now(),
        title: this.title,
        body: this.body,
      }
      this.posts.push(newPost);
      this.title = '';
      this.body = '';
    }
  },
  inputTitle(event) {
    this.title = event.target.value;
  }
}
</script>

<style scoped>
* {
   margin: 0;
   padding: 0;
   box-sizing: border-box;
}
.post {
   padding: 15px;
   border: 2px solid teal;
   margin-top: 15px;
}
form {
  display: flex;
  flex-direction: column;
}

.app {
  padding: 20px;
}
.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}
.btn {
  margin-top: 15px;
  align-self: flex-end;
  padding: 10px 15px;
  background: none;
  color: teal;
  border: 1px solid teal;
}
</style>
