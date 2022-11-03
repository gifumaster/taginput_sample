<script lang="ts">
export default {
  name: 'TagInput',
};
</script>

<script setup lang="ts">
import {computed, ref} from 'vue';
import ChipButton from "../atoms/ChipButton.vue";
import TextInput from "../atoms/TextInput.vue";

interface Props {
  modelValue: string[];
  label?: string;
}
const props = withDefaults(defineProps<Props>(),{
  label: 'タグをスペース区切りで入力してください'
});

const emits = defineEmits<{ (e: 'update:modelValue', value?: string): void }>();
const text = ref<string>('');

const inputValue = computed({
  get: () => props.modelValue,
  set: (value) => {
    emits('update:modelValue', value);
  },
});

const change = () => {
  const tagSource = inputValue.value.concat(text.value.split(' '));
  inputValue.value = Array.from(new Set(tagSource));
  text.value = '';
}

const remove = (text: string) => {
  inputValue.value = inputValue.value.filter((value) => value !== text)
}

</script>

<template>
  <TextInput v-model="text" :label="label" @change="change"></TextInput>
  <ChipButton v-for="text in inputValue" @click="remove(text)">{{ text }}</ChipButton>
</template>
