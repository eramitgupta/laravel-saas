<script setup>
import { ref } from 'vue';
import MultiSelect from 'primevue/multiselect';

const props = defineProps({
    modelValue: {
        type: Array,
        default: () => [],
    },
    options: {
        type: Array,
        required: true,
    },
    optionLabel: {
        type: String,
        required: true,
    },
    filter: {
        type: Boolean,
        default: true,
    },
    placeholder: {
        type: String,
        default: 'Select',
    },
    maxSelectedLabels: {
        type: Number,
        default: 3,
    },
});

const emit = defineEmits(['update:modelValue']);
const modelValue = ref(props.modelValue);

const handleUpdate = value => {
    modelValue.value = value;
    emit('update:modelValue', value);
};
</script>
<template>
    <div class="card flex justify-center">
        <MultiSelect
            :pt="{
                class: '!bg-dark',
            }"
            v-model="modelValue"
            :options="options"
            :optionLabel="optionLabel"
            :filter="filter"
            :placeholder="placeholder"
            :maxSelectedLabels="maxSelectedLabels"
            class="w-full md:w-60"
            @update:modelValue="handleUpdate"
        />
    </div>
</template>
