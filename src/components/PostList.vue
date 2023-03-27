<template>
  <div class="posts-list">
    <post-item @delete="deletePost" v-for="post in posts" :post="post" :key="post.id"/>
  </div>
</template>

<script>

import PostItem from "./PostItem.vue";
export default {
  name: "PostList",
  components: {PostItem},
  props:{
    posts:{
      type:Array,
      required:true
    }
  },
  methods:{
    deletePost(id){
      this.$emit('delete',id)
    }
  }
}
</script>

<style scoped>

</style>