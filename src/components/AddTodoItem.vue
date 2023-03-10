<template>
    <form @submit.prevent="onSubmit">
        <input type="text" v-model="title">
        <button type="submit">Create</button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            title: ''
        }
    },
    methods: {
        onSubmit() {
            if (this.title.trim()) {
                var newTodoItem = {
                    id: Date.now(),
                    title: this.title,
                    completed: false
                }

                this.$emit('add-todo-item', newTodoItem)
                this.title = ''
            }
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
    }

    input {
        width: 400px;
    }
</style>