<script setup>
import TodoCreator from "@/components/TodoCreator.vue";
import {ref} from "vue";
import {uid} from "uid";
import TodoItem from "@/components/TodoItem.vue";
import {Icon} from "@iconify/vue";

const todoList = ref([]);

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null,
  });
};
const toggleTodoComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
};

const toggleEditTodo = (todoPos) => {
  todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;
};

const updateTodo = (todoVal, todoPos) => {
  todoList.value[todoPos].todo = todoVal;
};
</script>

<template>
  <main>
    <h1>Create a Todo</h1>
    <TodoCreator @create-todo="createTodo"/>
    <ul class="todo-list" v-if="todoList.length > 0">
      <TodoItem
          v-for="(todo, index) in todoList"
          :todo="todo"
          :index="index"
          @toggle-complete="toggleTodoComplete"
          @edit-todo="toggleEditTodo"
          @update-todo="updateTodo"></TodoItem>
    </ul>
    <p class="todos-msg" v-else>
      <Icon icon="akar-icons:face-very-sad" width="22"/>
      <span>There are no todos to complete, please add one</span>
    </p>
  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style-type: none;
    margin-top: 25px;
    gap: 19px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 9px;
    margin-top: 25px;
    font-weight: bold;
  }
}
</style>
