<template>
<div class="app">
  <h1>Страница с постами</h1> 
  <MyInput 
  v-model:value="searchPost"
  placeholder="Поиск ..."
  /> 

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
  :posts="sortedAndSearchedPosts"
  @remove="removePost"> 
  </PostList>

 <div v-else class="loading">Идёт загрузка...</div>

<div class="page__wrapper">

  <div 
   v-for="pageNumber in totalPage" 
  :key="pageNumber" 
  class="page" 
  :class="{'cursor': page !== pageNumber, 'current-page': page === pageNumber,}"
  @click="changePage(pageNumber)"   
  > {{ pageNumber }} </div>
</div>

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
      ],
      page: 1,
      limit: 6,
      searchPost: "",
      totalPage: 0,
    } 
  },
  mounted(){
    this.fetchPosts();
  
  },
  computed:{
  sortedPost(){
    return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))  
  },
  sortedAndSearchedPosts(){
    return this.sortedPost.filter(post => post.title.toLowerCase().includes(this.searchPost.toLowerCase()))
  },
},

watch: {
  page(){
    this.fetchPosts()
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
    },
    fetchPosts(){
      try{
        this.isPostLoading = true;
        setTimeout(async() => {
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
          params:{
          _page: this.page,
          _limit: this.limit
        }       
      });
        this.totalPage = Math.ceil(Number(response.headers['x-total-count'])/this.limit)
        this.posts = response.data        
        this.isPostLoading = false;
        }, 800)

         
      } catch (e){
        alert("Ошибка")
      } 
    },
    changePage(pageNumber){
      this.page = pageNumber; 
    },
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
.page__wrapper{
  display: flex;
  margin: 15px;
}
.page{ 
  border: 1px solid black;
  padding: 10px;
}
.current-page{
  border: 2px solid teal;
}
.cursor{
  cursor: pointer;
}
.loading{
  font-size: larger;
  margin: 15px;
}
</style>
