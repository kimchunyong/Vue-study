
<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <Todoinput v-on:addTodo="addTodo"></Todoinput>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import Todoinput from './components/Todoinput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data(){
    return {
      todoItems:[]
    }
  },
  methods: {
    addTodo(todoItem) {
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    clearAll(){
        localStorage.clear();
        this.todoItems = []
    },
    removeTodo(todoItem, index){
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index, 1);
    }
  },
  created() {
      if(localStorage.length) {
          for(let i = 0; i < localStorage.length; i++) {
              this.todoItems.push(localStorage.key(i));
          }
      }
  },
  components: {
    'TodoHeader' : TodoHeader,
    'Todoinput' : Todoinput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter
  }
}

</script>

<style>
body {
  text-align: center;
  background-color: #f6f6f8;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>

