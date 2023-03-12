<template>
  <div v-if="posts.length">
    <h3>Список постов</h3>
    <PostItem 
    v-for="post in posts" 
    :post="post" 
    :key="post.id" 
    @remove="$emit('remove', post)"
   />    
  </div>

  <h3 v-else class="empty">Список постов пуст</h3>

</template>
  
  <script>
  import PostItem from "@/components/PostItem.vue"

  export default {
    name: 'PostList',  

    components: {PostItem},

    props: {
        posts:{
            type: Array,
            required: true,
        }
    }


  }
  </script>
  
  <style scoped>
  .post {
    padding: 15px;
    border: 2px solid teal;
    margin: 15px;
  }  
  .empty{
    color: red;
    text-align: center;
  }
  </style>
  