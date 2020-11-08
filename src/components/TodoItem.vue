<template>
    <li>
        <!-- Динамические классы -->
        <span :class="{done: todo.completed}">
            <input type="checkbox" @change="todo.completed = !todo.completed">
            <strong>{{ index + 1 }}</strong>
            {{ todo.title | uppercase }}
        </span>
        <!-- $emit - говорим род. объекту, что что-то случилось 1 - развание события, 2 - данные -->
        <button @click="$emit('remove-todo', todo.id)">&times;</button>
    </li>
</template>

<script>
export default {
    props: {
        // Принимаем todo в компонент
        todo: {
            type: Object,
            // Если объект не передан, то компонент не сможет работать
            required: true
        },
        index: Number
    },
    filters: {
        uppercase(val) {
            return val.toUpperCase();
        }
    }
}
</script>

<style lang="scss" scoped>
    li {
        border: 1px solid #ccc;
        display: flex;
        justify-content: space-between;
        padding: 0.5rem 2rem;
        margin-bottom: 1rem;

        input {
            margin-right: 1rem;
        }

        button {
            background-color: red;
            color: #fff;
            border-radius: 50%;
            border: none;
            font-weight: bold;
            cursor: pointer;
        }

        .done {
            text-decoration: line-through;
        }
    }
</style>