<template>
    <button
        class="submit"
    >
        <slot></slot>
    </button>
</template>

<style lang="scss" scoped>
@use "@/constants/mixins/borderStl.scss";
@use "@/constants/colors.scss";

.submit {
    padding: 16px 20px;
    font-size: 16px;
    color: white;
    border: none;
    border-radius: 0 10px 10px 0;
    background-color: colors.$primary;
    cursor: pointer;
    transition: 0.3s;
    @include borderStl.shadow;

    &.button {
        padding: 16px 30px;
        border-radius: 5px;
    }

    &.danger {
        background-color: colors.$danger;

        &:hover {
            background-color: red;
        }
    }

    &:hover {
        background-color: colors.$secondary;
        transition: 0.3s;
    }
}
</style>