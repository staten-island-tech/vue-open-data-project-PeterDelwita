<template>
  <div class="flex justify-center w-full">
    <CaseChart :apiUrl="apiUrl" />
  </div>
</template>

<script setup>
import CaseChart from '../components/CaseChart.vue'

const apiUrl = 'https://data.cityofnewyork.us/resource/rc75-m7u3.json'
</script>

<style scoped></style>
