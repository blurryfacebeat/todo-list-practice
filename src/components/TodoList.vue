<template>
    <div>
        <ul>
            <!-- :todo - байндим todo, чтобы передать дальше -->
            <TodoItem 
                v-for="(todo, index) of todos"
                :todo="todo"
                :index="index"
                :key="todo.id"
                @remove-todo="removeTodo"
            />
        </ul>
    </div>
</template>

<script>
import TodoItem from '@/components/TodoItem';

export default {
    // Указываем, что мы передаем из другого компонента (родительского, например)
    props: ['todos'],
    components: {
        TodoItem
    },
    methods: {
        // Метод для удаления элемента
        removeTodo(id) {
            console.log(id);
            this.$emit('remove-todo', id);
        }
    }
}
</script>

<style lang="scss" scoped>
    ul {
        list-style: none;
        margin: 0;
        padding: 0;
    }
</style>