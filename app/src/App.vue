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

onMounted(() => {
  getCasesPerDay()
})
// At least 2 charts (use chartjs)

// Process
// 1. Make the async function and fetch data
// 2. Decide which parts of the data should be used to make charts
// 3. Look at the API and use the data to make components (need to come back to this as I plan)

// Looking at the baby name project...
// There's a dropdown allowing you to select a name, which is accompanied by a chart. The chart should be a component
// There's a message while the charts load. The sidebar is in App.vue, while the rest is in its own view
</script>

<template>
  <!--API: https://data.cityofnewyork.us/resource/rc75-m7u3.json -->
  <h1 class="text-red-500 text-center text-[64px] font-bold">
    COVID-19 Daily Counts of Cases, Hospitalizations, and Deaths
  </h1>
</template>

<style scoped></style>
