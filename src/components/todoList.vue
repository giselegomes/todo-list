<template>
    <section class="todo">
        <header class="heading">
            <h1 class="heading__title">To-do List</h1>
        </header>
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
@import "@/assets/styles/_global.scss";

.material-symbols-outlined {
    font-variation-settings:
        'FILL' 0,
        'wght' 400,
        'GRAD' 0,
        'opsz' 48
}

.todo {
    background-color: $bg-color;

    .heading {
        display: flex;
        justify-content: center;

        .heading__title {
            font-size: 2em;
            font-family: 'Square Peg', cursive;
        }
    }

    .form {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 2%;

        .form__label {
            flex: 1 1 100%;
            text-align: center;
        }

        .form__input {
            row-gap: 10px;
        }

    }
}
</style>
