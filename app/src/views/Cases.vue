<template>
  <div>
    <h2>aaa</h2>
  </div>
</template>

<script setup>
// What to do here - make charts for cases here. Pie chart is impractical; make a bar chart for each borough
import { ref, onMounted } from 'vue'
const date = ref('')
async function getCasesPerDay() {
  try {
    let res = await fetch('https://data.cityofnewyork.us/resource/rc75-m7u3.json')
    let data = await res.json()
    console.log(data)
    // Log value and see what happens
    date.value = data
  } catch (error) {
    alert('Date not found')
  }
}

onMounted(() => {
  getCasesPerDay()
})
</script>

<style scoped></style>
