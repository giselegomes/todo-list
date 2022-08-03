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
                <li v-for="todo in todos" :key="todo.text" v-on:click="toggleTodo(todo)">
                    <input type="checkbox" :checked="todo.done">
                    <label>
                        <del v-if="todo.done">
                            {{ todo.text }}
                        </del>
                        <span v-else>
                            {{ todo.text }}
                        </span>
                    </label>
                    <span v-on:click="deleteTodo(todo)" class="material-symbols-outlined">close</span>
                </li>
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
        },
        toggleTodo(todo) {
            todo.done = !todo.done
        },
        deleteTodo(todo) {
            this.todos = this.todos.filter(el => el.text !== todo.text);
        }
    }
}
</script>

<style lang="scss">

@import "@/assets/styles/_variables.scss";

    .material-symbols-outlined {
        font-variation-settings:
            'FILL' 0,
            'wght' 400,
            'GRAD' 0,
            'opsz' 48
        }

    .list {
        color: $color;
    }
</style>
