<script setup>
    import {
        reactive,
        ref
    } from "vue";
    import TodoButton from "./TodoButton.vue";
    const todoState = reactive({
        todo: "",
        invalid: false,
        errMsg: ""
    });
    const emit = defineEmits(['create-todo']);
    const createTodo = () => {
        if (todoState.todo !== "") {
            todoState.invalid = false;
            emit("create-todo", todoState.todo);
            todoState.todo = "";
            return;
        }
        todoState.invalid = true;
        todoState.errMsg = "Todo Value can't be empty";
    }
</script>

<template>
    <form class="w-full max-w-lg">
        <div class="flex items-center border-b border-teal-500 py-2">
            <input class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none" type="text" placeholder="Todo Title" aria-label="Todo Title" v-model="todoState.todo" :class="{}" />
            <TodoButton @click="createTodo()">
                Create
            </TodoButton>
        </div>
    </form>
    <p v-show="todoState.invalid" class="err-msg mt-1">{{ todoState.errMsg }}</p>
</template>

<style lang="scss" scoped>
    .input-wrap {
        display: flex;
        transition: 250ms ease; //border: 2px solid #41b080;
        &.input-err {
            border-color: red;
        }
        &:focus-within {
            box-shadow: 0 -4px 5px -1px rgb(0 0 0 / 0.1), 0 -2px 4px -2px rgb(0 0 0 / 0.1);
        }
        input {
            width: 100%;
            padding: 8px 6px;
            &:focus {
                outline: none;
            }
        }
    }
    .err-msg {
        margin-top: 6px;
        font-size: 12px;
        color: red;
    }
</style>