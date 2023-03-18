<template>
    <input :value="value" @input="updateInput" type="text" class="input"/>
</template>
  
  <script>
  export default {
    name: 'MyInput',  
    props:{
        value: [String, Number]
    },
    methods:{
        updateInput(event){         
            this.$emit("update:value", event.target.value)
        }
    },
  }
  </script>
  
  <style scoped>

  .input {
    margin: 15px;
    border: 2px solid teal;
    padding: 10px; 
    }
  </style>
  