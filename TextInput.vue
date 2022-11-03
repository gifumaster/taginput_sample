<script lang="ts">
  export default {
    name: 'TextInput',
  };
</script>

<script setup lang="ts">
  import { computed } from 'vue';

  interface Props {
    modelValue: string;
    type?: 'text' | 'password';
    label?: string;
  }
  const props = defineProps<Props>();
  const emits = defineEmits<{ (e: 'update:modelValue', value?: string): void }>();

  const inputValue = computed({
    get: () => props.modelValue,
    set: (value) => {
      emits('update:modelValue', value);
    },
  });
</script>

<template>
  <v-text-field v-model="inputValue" :type="props.type" :label="props.label"></v-text-field>
</template>
