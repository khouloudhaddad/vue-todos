<script setup>
import TodoCreator from "../components/TodoCreator.vue";
</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <todoCreator />
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
      margin-bottom: 16px;
      text-align: center;
    }
  }
</style>
