<template>
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
        <p>
            <input type="checkbox" v-on:change="markComplete">
            {{ todo.title }} </p>
            <button @click="$emit('delete-todo', todo.id)" class="delete-button">X</button>
    </div>
</template>

<script>
export default {
    name: "TodoItem",
    props: ["todo"], 
    methods: {
        markComplete() {
            this.todo.completed = !this.todo.completed;
        }
    }
}

</script>
<style scoped>
    .todo-item {
        background: white;
        padding: 10px;
        border-bottom: 1px #ccc dotted;
    }
    .is-complete {
        text-decoration: line-through;
    }
    .delete-button {
        color: red;
    }
</style>