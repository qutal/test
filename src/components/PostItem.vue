<template>
  <div class="post">
    <div class="post-content">
      <h1  class="post-title">{{ post.title }}</h1>
      <p class="post-body">{{post.body}}</p>
    </div>
    <div class="post-buttons">
      <my-button @click="deletePost">Delete post</my-button>
    </div>
  </div>
</template>

<script>

export default {
  name: "PostItem",
  props:{
    post:{
      type:Object,
      required:true
    }
  },
  methods:{
    deletePost(){
      this.$emit('delete',this.post.id)
    }
  }
}
</script>

<style scoped>
.post{
  width: 100%;
  padding: 20px;
  border:1px solid teal;
  margin: 10px 0;
  display: grid;
  grid-template-columns: 9fr 1fr;
  grid-column-gap: 10px;
}
/*.post-content{*/
/*  width: 90%;*/
/*}*/

.post-buttons{
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.post-title{
  color:teal;
}

.post-body{
  color:teal;
}
</style>