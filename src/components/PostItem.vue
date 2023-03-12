<template>
    <div class="post">
        <div>
        <div> <strong> Название: </strong> {{post.title}} </div>
        <div> <strong> Описание: </strong> {{post.body}}</div> 
        </div>

        <div class="post__btn">
            <MyButtons @click="$emit('remove', post)">Удалить</MyButtons>
        </div>

    </div>
</template>
  
  <script>
import MyButtons from './UI/MyButtons.vue';

  export default {
    name: "PostItem",
    props: {
        post: {
            type: Object,
            required: true,
        }
    },
    components: { MyButtons },
  
}
  </script>
  
  <style scoped>
  .post {
    padding: 15px;
    border: 2px solid teal;
    margin: 15px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    
  }  

.btn {
    margin-top: 15px;    
    padding: 10px 15px;
    background: none;
    color: teal;
    border: 1px solid teal;
}
  </style>
  