<template>
  <div class="flex justify-center w-full">
    <HospitalizationChart :apiUrl="apiUrl" />
  </div>
</template>

<script setup>
import HospitalizationChart from '../components/HospitalizationChart.vue'

const apiUrl = 'https://data.cityofnewyork.us/resource/rc75-m7u3.json'
</script>

<style scoped></style>
