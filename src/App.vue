<template>
  <div class="app">
    <h1>post page</h1>
    <my-button
      @click="showDialog"
    >
      create a post
    </my-button>
    <my-dialog v-model:show="dialogVisible">
      <post-form
        @create="createPost"
      />
    </my-dialog>
    <post-list
      v-bind:posts="posts"
      @remove="removePost"
    />
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";

export default {
  components: {
    PostList, PostForm
  },
  data() {
    return {
      posts: [
         {id: 1, title: 'javascript1', body: 'post description1'},
         {id: 2, title: 'javascript2', body: 'post description2'},
         {id: 3, title: 'javascript3', body: 'post description3'}
      ],
      dialogVisible: false,
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showDialog() {
      this.dialogVisible = true;
    }
  }
}
</script>

<style>
* {
   margin: 10;
   padding: 10;
   box-sizing: border-box;
}
</style>
