<template>
  <div v-if="posts.length > 0">
    <h3>A list of posts</h3>
    <post-item
      v-for="post in posts"
      v-bind:post="post"
      v-bind:key="post.id"
      @remove="$emit('remove', post)"
    />
  </div>
  <h2 v-else style="color: red">
    post list is empty
  </h2>
</template>

<script>
import PostItem from "@/components/PostItem";
export default {
  components: {PostItem},
  props: {
    posts: {
      type: Array,
      required: true,
    }
  }
}
</script>

<style scoped>
div {
  padding: 15px;
}
</style>