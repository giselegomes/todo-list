<template>
    <section>
        <div class="heading">
            <h1 class="heading__title">To-do List</h1>
        </div>
        <form class="form">
            <label class="form__label">Today I need to:</label>
            <input v-model="currentTodo" class="form__input" type="text" size="30" required>
            <button v-on:click.prevent="newTodo" class="form__button">Submit</button>
        </form>
        <div class="list">
            <ul>
                <li v-for="todo in todos" :key="todo.text">{{ todo.text }}</li>
            </ul>
        </div>
    </section>
</template>

<script>
export default {
    data() {
        return {
            currentTodo: "",
            todos: []
        }
    },
    methods: {
        newTodo() {
            this.todos.push({
                text: this.currentTodo,
                done: false
            });
            this.currentTodo = "";
        }
    }
}
</script>