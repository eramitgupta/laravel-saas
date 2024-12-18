<script setup>
import { computed } from 'vue';
import CommonIcon from '@/Components/Common/CommonIcon.vue';

const props = defineProps({
    disabled: {
        type: Boolean,
        default: false,
    },
    icon: {
        type: [String, null],
    },
    trailingIcon: {
        type: [String, null],
    },
    size: {
        type: String,
        default: 'base',
    },
    type: {
        type: String,
        default: 'button',
    },
    processing: {
        type: Boolean,
        default: false,
    },
    variant: {
        type: String,
        default: 'primary',
    },
    rounded: {
        type: Boolean,
        default: false,
    },
});

const isDisabled = computed(() => {
    return props.disabled || props.processing;
});

const sizingClasses = computed(() => {
    return {
        xs: 'p-2 text-sm',
        sm: 'p-3 text-sm',
        base: props.rounded ? 'text-base' : 'px-3 py-2  text-base',
        lg: 'p-3 text-lg',
    };
});

const sizeClass = computed(() => {
    return sizingClasses.value[props.size];
});

const disabledClass = computed(() => {
    return props.disabled ? 'bg-gray-300 text-gray-500 cursor-not-allowed' : '';
});

const roundedClass = computed(() => {
    return props.rounded ? 'rounded-full' : 'rounded-md';
});

const variants = {
    primary:
        'bg-indigo-700 hover:bg-indigo-600 text-white border border-transparent focus-visible:ring-2 focus-visible:ring-indigo-700 ring-offset-1 active:bg-indigo-900',
    secondary:
        'bg-transparent text-teal-700 border border-teal-700 focus-visible:ring-2 focus-visible:ring-teal-700 ring-offset-1 active:text-teal-300',
    gray: 'bg-gray-100 text-gray-700 border border-transparent focus-visible:ring-2 focus-visible:ring-teal-700 ring-offset-1 active:text-gray-300',
    transparent:
        'bg-transparent text-gray-700 border border-transparent focus-visible:ring-2 focus-visible:ring-teal-700 ring-offset-1 active:text-gray-300',
    danger: 'bg-transparent text-red-700 border border-red-700 hover:ring-red-600 hover:text-red-600 focus-visible:ring-2 focus-visible:ring-red-700 ring-offset-1',
};

const variantClass = computed(() => {
    return variants[props.variant];
});
</script>

<template>
    <button
        :disabled="isDisabled"
        class="relative inline-flex items-center justify-center gap-2 font-medium leading-snug transition-colors focus:outline-none disabled:cursor-not-allowed disabled:opacity-75"
        :class="[sizeClass, disabledClass, variantClass, roundedClass]"
        :type="type"
    >
        <CommonIcon v-if="icon" :icon="icon" class="h-5 w-5" />
        <slot />
        <CommonIcon v-if="trailingIcon" :icon="trailingIcon" class="h-5 w-5" />

        <Transition
            enter-active-class="transition ease-out duration-100"
            enter-from-class="transform opacity-0 scale-95"
            enter-to-class="transform opacity-100 scale-100"
            leave-active-class="transition ease-in duration-75"
            leave-from-class="transform opacity-100 scale-100"
            leave-to-class="transform opacity-0 scale-95"
        >
            <div v-if="processing" class="absolute inset-0 flex h-full w-full">
                <div
                    class="flex h-full w-full items-center justify-center rounded bg-indigo-700 bg-opacity-80"
                >
                    <CommonIcon
                        class="h-5 w-5 animate-spin"
                        icon="fa6-solid:spinner"
                    />
                </div>
            </div>
        </Transition>
    </button>
</template>
