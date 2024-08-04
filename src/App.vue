<script setup lang="ts">
import { ref } from 'vue';
import MoneyInput from './components/MoneyInput.vue'

const amount = ref<string>('');
</script>

<template>
 <main class="p-4">
    <MoneyInput v-model="amount" />

    <p class="mt-4 text-gray-700">Montant enregistré: {{ amount }}</p>
  </main>
</template>
