<template>
    <form @submit.prevent>
        <h4>Creating a post</h4>
        <my-input
            v-focus
            v-model="post.title"
            type="text"
            placeholder="post title"
        />
        <my-input
            v-model="post.body"
            type="text"
            placeholder="post description"
        />
        <my-button
            class="btn"
            style="align-self: flex-end; margin-top: 15px"
            @click="createPost"
        >
            Create
        </my-button>
    </form>
</template>

<script>
export default {
  data() {
    return {
      post: {
         title: '',
         body: ''
      }
    }
  },
  methods: {
    createPost() {
        this.post.id = Date.now();
        this.$emit('create', this.post)
        this.post = {
           title: '',
           body: ''
        }
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  padding: 15px;
}


</style>

