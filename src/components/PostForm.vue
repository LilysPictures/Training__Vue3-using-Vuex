<template>
    <form @submit.prevent>
        
        <h4>Создание поста</h4>

        <MyInput    
        v-model:value="post.title"    
        placeholder="Название"/>

        <MyInput 
        v-model:value="post.body"
        placeholder="Описание"/>

        <button class="btn" @click="createPost">Создать</button>

    </form>
</template>
  
  <script>
  export default {
    name: 'PostForm',  
    data(){
        return {
            post:{
                title: "",
                body: "",
            }
        }
    },
    methods:{
      createPost(){
        this.post.id = Date.now();
        this.$emit("create", this.post);
        // this.posts.push(newPost),
        this.post = {
          title: '',
          body: '',
        }       
    },
    }
  }
  </script>
  
  <style scoped>
  form {
    padding: 15px;
    display: flex;
    flex-direction: column;
  }  
  .btn {
    margin-top: 15px;
    align-self: self-end;
    padding: 10px 15px;
    background: none;
    color: teal;
    border: 1px solid teal;
    }  
  </style>
  