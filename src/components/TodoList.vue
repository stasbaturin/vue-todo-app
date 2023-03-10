<template>
    <div>
        <ul>
            <TodoItem 
                v-for="(todo, i) of todos"
                v-bind:todo="todo"
                v-bind:index="i"
                v-on:remove-item="removeItem"
            />
        </ul>
    </div>
</template>

<script>
import TodoItem from '@/components/TodoItem.vue';
export default {
    props: ['todos'],
    components: {
        TodoItem
    },
    methods: {
        removeItem(id) {
            this.$emit('remove-item', id)
        }
    }
}
</script>

<style scoped>
    ul {
        list-style: none;
        margin: 0;
        padding: 0;
    }
</style>