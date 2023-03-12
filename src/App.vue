<template>
<div class="app">
  <h1>Страница с постами</h1> 
  <MyButtons
  class="createBtn"
  @click="showDialog">Создать пост</MyButtons>
  <MyDialog v-model:show="dialogVisible" >
  <PostForm 
  @create="createPost"/>
</MyDialog>
  <PostList 
  :posts="posts"
  @remove="removePost"
  />
</div> 

</template>

<script>
import PostList from "@/components/PostList"
import PostForm from "./components/PostForm"
import MyButtons from "./components/UI/MyButtons.vue"

export default {  
  name: 'AppPage',

  components:{
    PostList,
    PostForm,
    MyButtons
},

  data() {
    return {
      posts: [
        {id: 1, title: "JavaScript", body: "Описание поста"},
        {id: 2, title: "JavaScript 1", body: "Описание поста 1"},
        {id: 3, title: "JavaScript 2", body: "Описание поста 2"},
      ],
      dialogVisible: false,
      modificatorValue: "",
    } 
  },

  methods:{ 
    createPost(post){
     this.posts.push(post)
     this.dialogVisible = false
    },
    removePost(post){    
      this.posts = this.posts.filter(p=> p.id != post.id)
    },
    showDialog(){
      this.dialogVisible = true

    }
  }
}

</script>


<style>
.app{
  padding: 15px;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.createBtn{
  margin: 15px;
}
</style>
