<template>
<div class="app">
  <PostForm 
  @create="createPost"/>
  <PostList 
  :posts="posts"
  />
</div> 

</template>

<script>
import PostList from "@/components/PostList"
import PostForm from "./components/PostForm"

export default {  
  name: 'AppPage',

  components:{
    PostList, PostForm
  },

  data() {
    return {
      posts: [
        {id: 1, title: "JavaScript", body: "Описание поста"},
        {id: 2, title: "JavaScript 1", body: "Описание поста 1"},
        {id: 3, title: "JavaScript 2", body: "Описание поста 2"},
      ],
    } 
  },

  methods:{ 
    createPost(post){
     this.posts.push(post)
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
</style>
