<template>
  <TodoHeader :appTitle="title"></TodoHeader>
  <TodoInput @add="addTodoItem"></TodoInput>
  <TodoList :todoItems="todoItems" @remove="removeTodoItem"></TodoList>
</template>

<script>
import TodoHeader from '@/components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import { useTodo } from './hooks/useTodo';
import { onBeforeMount } from 'vue';

  export default {
    components: {
      TodoHeader,
      TodoInput,
      TodoList,
    },
    data() {
      return {
        title: '할일 앱'
      }
    },
    setup() {
      const { todoItems, fetchTodos, addTodoItem } = useTodo();

      onBeforeMount(() => {
        console.log("onBeforeMount called");
        todoItems.value = fetchTodos();
      })
      
      console.log("setup called");
      
      return { todoItems, addTodoItem }
    },
    methods: {
      removeTodoItem(item, index) {
        this.todoItems.splice(index, 1);
        localStorage.removeItem(item);
      }
    }

    
  }
</script>

<style lang="scss" scoped>

</style>