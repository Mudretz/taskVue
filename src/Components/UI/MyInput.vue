<script setup lang="ts">

interface Props {
    modelValue: string
}

interface Emits {
    (e: "update:modelValue", text: string): void
}

defineProps<Props>();
const emit = defineEmits<Emits>();

const updateValue = (event: Event) => {
  const newValue = (event.target as HTMLInputElement).value
  emit('update:modelValue', newValue)
};

</script>

<template>
    <input
        :value="modelValue"
        class="input"
        @input="updateValue"
    >
</template>

<style scoped lang="scss">
@use "@/constants/mixins/borderStl.scss";
@use "@/constants/colors.scss";

    .input {
        padding: 16px 20px;
        box-sizing: border-box;
        width: 100%;
        border-radius: 10px 0 0 10px;
        border: none;
        font-size: 16px;
        @include borderStl.shadow;

        &:focus {
            outline: 0;
            box-shadow: 0 0 0 2px #87b7ff;
        }
    }
</style>