<template>
  <div v-if="posts.length">
    <h3>Список постов</h3>
    <transition-group name="post-list">
    <PostItem 
    v-for="post in posts" 
    :post="post" 
    :key="post.id" 
    @remove="$emit('remove', post)"
   />    
  </transition-group>
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

  .post-list-item {
    display: inline-block;
    margin-right: 10px;
  }
  .post-list-enter-active,
  .post-list-leave-active {
    transition: all 1s ease;
  }
  .post-list-enter-from,
  .post-list-leave-to {
    opacity: 0;
    transform: translateY(30px);
  }
  .post-list-move {
    transition: transform 0.4s ease;
  }
  </style>
  