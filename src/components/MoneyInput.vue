<script setup lang="ts">
import { ref, computed, watch } from 'vue';

defineProps<{ modelValue: string }>();
const emit = defineEmits(['update:modelValue']);

const rawValue = ref('');
const formattedValue = computed(() => rawValue.value.replace(/\B(?=(\d{3})+(?!\d))/g, ' '));

watch(rawValue, () => emit('update:modelValue', formattedValue.value));

const handleInput = (event) => {
    const input = event.target.value.replace(/\s+/g, '');

    if (/^\d*$/.test(input)) {
        rawValue.value = input;
        return;
    }
    
    event.target.value = formattedValue.value;
};
</script>

<template>
    <div>
        <label for="price" class="block text-sm font-medium leading-6 text-gray-900">Prix</label>
        <div class="relative mt-2 rounded-md shadow-sm">
            <div class="pointer-events-none absolute inset-y-0 left-0 flex items-center pl-3">
                <span class="text-gray-500 sm:text-sm">€</span>
            </div>
            <input
                @input="handleInput"
                :value="formattedValue"
                type="text"
                name="price"
                id="price"
                class="block w-full rounded-md border-0 py-1.5 pl-7 pr-12 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                placeholder="10 000"
                aria-describedby="price-currency"
            >
            
            <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center pr-3">
                <span class="text-gray-500 sm:text-sm" id="price-currency">EUR</span>
            </div>
        </div>
    </div>
</template>
