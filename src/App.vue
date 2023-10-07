<script setup lang="ts">
import {ref} from "vue";
import type {Todo} from "@/types";
import CardTodo from "@/Components/Common/CardTodo.vue";
import MyButton from "@/Components/UI/MyButton.vue";
import MyInput from "@/Components/UI/MyInput.vue";

const todo = ref<string>("");

const todoList = ref<Todo[]>([
        {
            id: 1,
            text: "Сделать домашнее задание на Vue",
            status: true
        },
        {
            id: 2,
            text: "Сделать проект на Vue",
            status: false
        }
    ]
);

const addTodo = () => {
    if (todo.value.trim() === "") {
        return null
    } else {
        todoList.value.push({
            id: Date.now(),
            text: todo.value,
            status: false
        });
        todo.value = "";
    }
};

const deleteTodo = (id: number) => {
    todoList.value = todoList.value.filter((item) => item.id !== id);
};

const completedTodo = (id: number) => {
    const index = todoList.value.findIndex((item) => item.id === id);
    todoList.value[index] = { ...todoList.value[index], status: true};
};

</script>

<template>
    <div class="container">
        <form class="form" @submit.prevent="addTodo">
            <label for="todo" class="title">Введите задачу</label>
            <div class="inputGroup">
                <MyInput v-model="todo"/>
                <MyButton
                    type="submit"
                >
                    Добавить
                </MyButton>
            </div>
            <CardTodo
                v-for="todo in todoList"
                :key="todo.id"
                :todo="todo"
                @completedTodo="completedTodo"
                @deleteTodo="deleteTodo"
            />
        </form>
    </div>
</template>

<style scoped lang="scss">
@use "@/constants/colors";
@use "@/constants/mixins/borderStl";

    .container {
        height: 100vh;
        width: 100%;
        display: flex;
        justify-content: center;
        background-color: colors.$bgColor;
    }

    .form {
        margin-top: 100px;
        width: 500px;
        display: flex;
        flex-direction: column;
        row-gap: 20px;
    }

    .title {
        font-size: 24px;
    }

    .inputGroup {
        display: flex;
    }
</style>
