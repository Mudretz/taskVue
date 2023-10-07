<script setup lang="ts">
import type {Todo} from "@/types";
import deleteIcon from "@/Assets/icons/delete.svg";
import checkIcon from "@/Assets/icons/check.svg";

interface Emits {
    (e: "completedTodo", id: number): void,
    (e: "deleteTodo", id: number): void
}

interface Props {
    todo: Todo
}

defineEmits<Emits>();
defineProps<Props>();

</script>

<template>
    <div class="card">
        <div class="textBlock">
            <p class="text">{{ todo.text }}</p>
            <div class="line" :class="{ active: todo.status }"></div>
        </div>
        <div class="iconGroup">
            <img
                :src="deleteIcon"
                alt="удалить"
                class="icon delete"
                @click="$emit('deleteTodo', todo.id)"
            >
            <img
                v-show="!todo.status"
                :src="checkIcon"
                alt="выполено"
                class="icon check"
                @click="$emit('completedTodo', todo.id)"
            >
        </div>
    </div>
</template>

<style lang="scss" scoped>
@use "@/constants/colors";
@use "@/constants/mixins/borderStl";

.card {
    padding: 0 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    column-gap: 30px;
    @include borderStl.shadow;
}

.line {
    position: absolute;
    width: 0;
    border-top: 2px solid black;
    transition: 0.3s;

    &.active {
        width: 100%;
        transition: 0.3s;
    }
}

.textBlock {
    position: relative;
    display: flex;
    align-items: center;
    font-size: 20px;
    word-break: break-word;
}

.iconGroup {
    display: flex;
    column-gap: 10px;
}

.icon {
    padding: 2px;
    width: 20px;
    cursor: pointer;
    border: 2px solid colors.$bgColor;
    border-radius: 5px;
    transition: 0.3s;

    &:hover {
        border-width: 2px;
        border-style: solid;
        transition: 0.3s;

        &.delete {
            border-color: colors.$danger;
        }

        &.edit {
            border-color: colors.$primary;
        }

        &.check {
            border-color: colors.$success;
        }
    }
}
</style>