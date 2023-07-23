<script setup>
    import {
        reactive,
        ref
    } from "vue";
    const todoState = reactive({
        todo: "",
        invalid: "",
        errMsg: ""
    });
    const emit = defineEmits(['create-todo']);
    const createTodo = () => {
        if (todoState.todo !== "") {
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
            <input class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none" type="text" placeholder="Todo Title" 
            aria-label="Todo Title" v-model="todoState.todo" />
            <button class="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded" 
            type="button"
            @click="createTodo()">
                Create
            </button>
        </div>
    </form>
    
    <p class="err-msg mt-1">{{ todoState.errMsg }}</p>
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