<template>
  <form @submit.prevent>
    <h4>Создание поста</h4>
    <my-input v-model="post.title"/>
    <my-input v-model="post.body"/>
    <my-button @click="createPost">Создать пост</my-button>
  </form>
</template>

<script>

export default {
  name: "PostForm",
  data(){
    return {
      post:{
        title:'',
        body:''
      }
    }
  },
  methods:{
    createPost(){

      const newPost = {
        id:Date.now(),
        title:this.post.title,
        body:this.post.body
      }
      this.$emit('create',newPost)
      this.post.title=''
      this.post.body = ''
    }
  }
}
</script>

<style scoped>

</style>