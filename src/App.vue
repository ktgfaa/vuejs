<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:propsData="todoItems" @removeTodo="removeTodo" @fixTodo="fixTodo"></TodoList>
    <TodoFooter v-on:clearAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
  import TodoHeader from './components/TodoHeader.vue'
  import TodoInput from './components/TodoInput.vue'
  import TodoList from './components/TodoList.vue'
  import TodoFooter from './components/TodoFooter.vue'

export default {
  data(){
    return {
      todoItems:[]
    }
  },
  created() {
    if(localStorage.length > 0) {
      for(let i = 0;localStorage.length > i;i++){
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  methods : {
    addTodo(todoItem) {
      localStorage.setItem(todoItem,todoItem);
      this.todoItems.push(todoItem);
    },
    clearAll() {
      localStorage.clear();
      this.todoItems=[];
    },
    removeTodo(todoItem,index){
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index,1);
    },
    fixTodo(todoItem,index){
      const fxkey = document.getElementsByClassName('fix').item(index).value;
      if(fxkey !== todoItem){
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index,1);

      localStorage.setItem(fxkey,fxkey);
      this.todoItems.push(fxkey);
      }
      
    }
  },
  components : {
    'TodoHeader' : TodoHeader,
    'TodoInput' : TodoInput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter
  }
}
</script>

<style>
  body {
    text-align: center;
    background-color: #F6F6F8;
  }
  input {
    border-style: groove;
    width : 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0,0,0,0.3);
  }

</style>
