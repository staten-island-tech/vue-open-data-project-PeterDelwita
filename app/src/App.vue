<script setup>
import { RouterLink, RouterView } from 'vue-router'

import { ref, onMounted } from 'vue'
const day = ref('')
async function getCasesPerDay() {
  try {
    let res = await fetch('https://data.cityofnewyork.us/resource/rc75-m7u3.json')
    let data = await res.json()
    day.value = data.results
  } catch (error) {
    alert('Date not found')
  }
}
// At least 2 charts (use chartjs)

// Process
// 1. Make the async function and fetch data
// 2. Decide which parts of the data should be used to make charts
// 3. Look at the API and use the data to make components
</script>

<template>
  <!--API: https://data.cityofnewyork.us/resource/rc75-m7u3.json -->
  <h1 class="text-red-500 text-center text-[64px] font-bold">
    COVID-19 Daily Counts of Cases, Hospitalizations, and Deaths
  </h1>
</template>

<style scoped></style>
