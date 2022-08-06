<template>
    <section class="container">
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
                <li class="list__item" v-for="todo in todos" :key="todo.text" v-on:click="toggleTodo(todo)">
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

body {
    background-color: $bg-color;
    min-height: 60vh;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;

    @include desktop {
        min-height: 100vh;
    }
}

.container {
    background-color: $bg-todo-color;
    width: 95%;
    height: auto;
    min-height: 500px;
    margin: 0 auto;
    border-radius: 22px;
    box-shadow: 4px 3px 7px 2px #00000040;

    .heading {
        display: flex;
        justify-content: center;

        .heading__title {
            font-size: 4em;
            font-family: 'Square Peg', cursive;
            color: $title-color;
            margin: 0;
            padding: 0.5rem 0;
        }
    }

    .form {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 2%;

        .form__label {
            font-family: 'Indie Flower', cursive;
            padding: 0.5rem 0;
            font-weight: bold;
            flex: 1 1 100%;
            text-align: center;
        }

        .form__input {
            row-gap: 10px;
            border: 2px solid $pink;
            height: 3.5vh;
            max-width: 200px;
        }

        .form__button {
            border: none;
            background: none;
            font-family: "Indie Flower", cursive;
            font-size: 1rem;
            font-weight: bold;

            &:hover {
                font-style: italic;
                text-decoration: underline;
            }
        }

    }

    .list {
        ul {
            padding: 1.5rem 0;
            max-width: 75%;
            margin: 0 auto;

            .list__item {
                list-style: none;
                display: flex;
                justify-content: flex-start;
                font-family: "Indie Flower", cursive;

                span {
                    font-weight: bold;
                    font-size: 1rem;
                    padding: 0 1rem 0 0.25rem;
                }

                label del {
                    font-weight: bold;
                    font-style: italic;
                    padding: 0 1rem 0 0.25rem;
                }
            }
        }
    }
}
</style>
