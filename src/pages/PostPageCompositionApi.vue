<template>
  <div>
    <h1>post page</h1>
    <my-input
      v-focus
      v-model="searchQuery"
      placeholder="Post search..."
    />
    <div class="app__btns">
        <my-button
        >
          create a post
        </my-button>
        <my-select
          v-model="selectedSort"
          :options="sortOptions"
        />
    </div>
    <my-dialog v-model:show="dialogVisible">
      <post-form
      />
    </my-dialog>
    <post-list
      v-bind:posts="sortedAndSearchedPosts"
      v-if="!isPostsLoading"
    />
    <div v-else>Loading process</div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import axios from 'axios';
import {ref} from 'vue'
import {usePosts} from "@/hooks/usePosts";
import useSortedPosts from "@/hooks/useSortedPosts";
import useSortedAndSearchedPosts from "@/hooks/useSortedAndSearchedPosts";

export default {
  components: {
    PostList, PostForm
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      sortOptions: [
        {value: 'title', name: 'By name'},
        {value: 'body', name: 'By content'},
      ]
    }
  },
  setup(props) {
    const {posts, totalPages, isPostsLoading} = usePosts(10);
    const {sortedPosts, selectedSort} = useSortedPosts(posts);
    const {searchQuery, sortedAndSearchedPosts} = useSortedAndSearchedPosts(sortedPosts);

    return {
        posts,
        totalPages,
        isPostsLoading,
        sortedPosts,
        selectedSort,
        searchQuery,
        sortedAndSearchedPosts
    }
  }
}

</script>

<style>

.app__btns {
   margin: 15px 0;
   display: flex;
   justify-content: space-between;
}
.page__wrapper {
   display: flex;
   margin-top: 15px;
}
.page {
   border: 1px solid black;
   padding: 10px;
}
.current-page {
   border: 3px solid red;
}
.observer {
   height: 10px;
}
</style>
