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
  const todosCompleted = computed(() => {
    return todoList.value.every((todo) => todo.isCompleted);
  });
  const fetchTodoList = () => {
    const savedTodoList = JSON.parse(localStorage.getItem("todoList"));
    if (savedTodoList) {
      todoList.value = savedTodoList;
    }
  };
  // Fetch Todo's on page load
  fetchTodoList();
  const createTodo = (todo) => {
    console.log(todo)
    todoList.value.push({
      id: uid(),
      todo,
      isCompleted: false,
      isEditing: false
    });
    setTodoListLocalStorage();
  }
  const toggleEditTodo = (todoPos) => {
    todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;
    setTodoListLocalStorage();
  };
  const updateTodo = (todoVal, todoPos) => {
    todoList.value[todoPos].todo = todoVal;
    setTodoListLocalStorage();
  };
  const toggleTodoComplete = (todoPos) => {
    todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
    setTodoListLocalStorage();
  };
  const deleteTodo = (todo) => {
    todoList.value = todoList.value.filter(
      (todoFilter) => todoFilter.id !== todo.id
    );
    setTodoListLocalStorage();
  };
</script>

<template>
  <main>
    <h1 class="font-bold text-2xl mb-16 text-gray-700">Create Todo</h1>
    <TodoCreator @create-todo="createTodo" />
    <ul class="todo-list" v-if="todoList.length > 0">
      <TodoItem v-for="(todo, index) in todoList" :todo="todo" :index="index" @edit-todo="toggleEditTodo" @update-todo="updateTodo" @toggle-complete="toggleTodoComplete" @delete-todo="deleteTodo" :key="todo.id" />
    </ul>
    <p v-else class="todos-msg">
      <Icon icon="noto-v1:sad-but-relieved-face" />
      <span>You have no todo's to complete! Add one!</span>
    </p>
    <p v-if="todosCompleted && todoList.length > 0" class="todos-msg">
      <Icon icon="noto-v1:party-popper" />
      <span>You have completed all your todos!</span>
    </p>
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
