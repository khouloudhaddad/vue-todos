<script setup>
  import {
    ref
  } from "vue";
  import TodoCreator from "../components/TodoCreator.vue";
  import {
    uid
  } from 'uid';
  import TodoItem from "../components/TodoItem.vue";
  const todoList = ref([]);
  const createTodo = (todo) => {
    console.log(todo)
    todoList.value.push({
      id: uid(),
      todo,
      isCompleted: false,
      isEditing: false
    })
  }
</script>

<template>
  <main>
    <h1 class="font-bold text-2xl mb-16 text-gray-700">Create Todo</h1>
    <TodoCreator @create-todo="createTodo" />
    <div class="todoslist">
      <ul class="list-none">
        <TodoItem v-for="todo in todoList" :key="todo.id" :todo="todo" />
      </ul>
    </div>
  </main>
</template>

<style lang="scss" scoped>
  main {
    display: flex;
    flex-direction: column;
    max-width: 500px;
    width: 100%;
    margin: 0 auto;
    padding: 40px 16px;
    h1 {
      text-align: center;
    }
  }
</style>
