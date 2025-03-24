<template>
  <div class="about">
    <DeathChart :apiUrl="apiUrl" />
  </div>
</template>

<script setup>
import DeathChart from '../components/DeathChart.vue'

const apiUrl = 'https://data.cityofnewyork.us/resource/rc75-m7u3.json'
</script>

<style scoped></style>
