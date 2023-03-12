<template>
<div class="app">
  <h1>Страница с постами</h1> 
<div class="app__buttons">
 
  <MyButtons
  class="createBtn"
  @click="showDialog">
  Создать пост
  </MyButtons>

  <MySelect 
  v-model="selectedSort"
  :options="sortOptions"
  ></MySelect>


</div>

  <MyDialog v-model:show="dialogVisible" >
  <PostForm 
  @create="createPost"/>
  </MyDialog>

  <PostList 
  v-if="!isPostLoading"
  :posts="posts"
  @remove="removePost"> 
  </PostList>

 <div v-else>Идёт загрузка...</div>

</div> 

</template>

<script>
import PostList from "@/components/PostList"
import PostForm from "./components/PostForm"
import MyButtons from "./components/UI/MyButtons.vue"
import axios from "axios"
import MySelect from "./components/UI/MySelect.vue"

export default {  
  name: 'AppPage',

  components:{
    PostList,
    PostForm,
    MyButtons,
    MySelect
},

  data() {
    return {
      posts: [],
      dialogVisible: false,
      modificatorValue: "",
      isPostLoading: false,
      selectedSort: "",
      sortOptions: [
        {value: "title", name: "По названию"},
        {value: "body ", name: "По содержимому"},
      ]

    } 
  },
  mounted(){
    this.fetchPosts();
  },

  watch:{
    selectedSort(newValue){
      this.posts.sort((post1, post2)=>{
        return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
      })    
    },
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
    },
    async fetchPosts(){
      try{
        this.isPostLoading = true;
        setTimeout(async() => {
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
        this.posts = response.data
        this.isPostLoading = false;
        }, 1000)       
        
      } catch (e){
        alert("Ошибка")
      } 
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
.app__buttons{
  display: flex;
  justify-content: space-between;
}
</style>
