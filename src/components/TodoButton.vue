<script setup>

</script>

<template>
    <button class="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded" type="button" @click="createTodo()">
        <slot></slot>
    </button>
</template>

<style lang="scss" scoped>
    button {
        padding: 8px 16px;
        border: none;
    }
</style>