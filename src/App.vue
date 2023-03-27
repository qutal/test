<template>
  <my-dialog v-model:show="dialogShow">
    <PostForm  @create="createPost"/>
  </my-dialog>

  <div class="wrapper">
    <div class="app_btns">
      <my-button @click="e=>{dialogShow=true}">Создать пост</my-button>
      <my-select
        v-model="selectedSort"
        :options="sortOptions"
      />
    </div>

    <div v-if="posts.length>0">
      <PostList
          v-if="!isPostsLoading"
          :posts="posts"
          @delete="deletePost"
      />

    </div>
    <div v-if="isPostsLoading">Идет загрузка...</div>
    <h1 v-if="posts.length===0 && !isPostsLoading">Постов нет</h1>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import axios from 'axios'
export default {
  name: "App",
  components: {PostForm,PostList},
  data(){
    return {
      posts:[],
      dialogShow:false,
      isPostsLoading:false,
      selectedSort:'',
      sortOptions:[
        {
          value:'title',
          name:'Заголовок'
        },
        {
          value:'body',
          name:'Текст'
        },
      ]
    }
  },
  methods:{
    createPost(post){
      this.posts.push(post)
    },
    deletePost(id){
      this.posts = this.posts.filter(post=>{
        return post.id!==id
      })
    },
    async fetchUsers(){
      try{
        this.isPostsLoading=true
        setTimeout(async ()=>{
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts/?_limit=10')
          this.posts = response.data
          this.isPostsLoading=false
        },1000)

      }catch (error){
        alert('Ошибка '+error.message)
      }
    }
  },




  mounted() {
    this.fetchUsers()
  },
  watch:{
    selectedSort(newValue){
      console.log('watch')
      console.log(newValue)
    }
  }
}
</script>

<style>
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .wrapper{
    width: 80%;
    margin: auto;
    padding-top: 20px;
  }

  form{
    width: 100%;
    padding: 10px;
  }

  .app_btns{
    display: flex;
    justify-content: space-between;
  }
</style>