<script setup lang="ts">
import { ref } from 'vue';


const currencyFrom = ref('USD');
const currencyTo = ref('USD');

const result = ref('');

const check = () => {
  fetch(`https://api.exchangerate-api.com/v4/latest/${currencyFrom.value}`)
    .then(response => response.json())
    .then(data => {
      result.value = `Aktualny kurs ${currencyFrom.value} do ${currencyTo.value}: ${data.rates[currencyTo.value]}`;
    })
    .catch(error => {
      console.error('Błąd podczas pobierania kursu:', error);
    });
};
</script>

<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gray-100">
    <h1 class="text-4xl font-bold mb-4">Kursy Walut</h1>
    <p class="text-lg mb-8">Wybierz walutę, aby zobaczyć aktualny kurs</p>
    <div class="w-full max-w-md">
      <label for="currency" class="block text-sm font-medium text-gray-700 mb-2">Wybierz walutę:</label>
      <select v-model="currencyFrom" id="currency" class="block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500">
        <option value="USD">USD</option>
        <option value="PLN">PLN</option>
        <option value="EUR">EUR</option>
        <option value="GBP">GBP</option>
        <option value="CHF">CHF</option>
        <option value="JPY">JPY</option>
      </select>
      <label for="currency" class="block text-sm font-medium text-gray-700 mb-2">Docelowa waluta:</label>
      <select v-model="currencyTo" id="target-currency" class="block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500">
        <option value="PLN">PLN</option>
        <option value="USD">USD</option>
        <option value="EUR">EUR</option>
        <option value="GBP">GBP</option>
        <option value="CHF">CHF</option>
        <option value="JPY">JPY</option>
      </select>
      <button @click="check" class="mt-4 w-full bg-blue-600 text-white p-2 rounded-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2">
        Sprawdź kurs
      </button>
      <div class="mt-4 text-center text-green-500 text-xl font-bold">
        <p class="">{{ result }}</p>
      </div>
      <div class="mt-4 text-center">
        <p class="text-sm text-gray-500">Aplikacja korzysta z danych www.exchangerate-api.com.</p>
      </div>
    </div>
  </div>
</template>

