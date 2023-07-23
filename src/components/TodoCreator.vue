<script setup>
    import {
        ref
    } from "vue";
    const todo = ref("");
    const emit = defineEmits(['create-todo']);
    const createTodo = () => {
        emit("create-todo", todo.value);
    }
</script>

<template>
    <div class="input-wrap">
        <input type="text" v-model="todo" />
        <button @click="createTodo()">Create</button>
    </div>
</template>

<style lang="scss" scoped>
    .input-wrap {
        display: flex;
        transition: 250ms ease;
        border: 2px solid #41b080;
        &.input-err {
            border-color: red;
        }
        &:focus-within {
            box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1), 0 -2px 4px -2px rgb(0 0 0 / 0.1);
        }
        input {
            width: 100%;
            padding: 8px 6px;
            border: none;
            &:focus {
                outline: none;
            }
        }
        button {
            padding: 8px 16px;
            border: none;
        }
    }
    .err-msg {
        margin-top: 6px;
        font-size: 12px;
        text-align: center;
        color: red;
    }
</style>