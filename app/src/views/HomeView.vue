<template>
  <div>
    <div class="button-container flex flex-wrap justify-center w-full">
      <details class="dropdown">
        <summary
          class="btn text-[32px] p-2 rounded-lg border-red-600 border-solid border-2 bg-white text-red-600 hover:bg-gray-950 hover:text-red-500 hover:border-red-600 hover:shadow-red-600/90"
        >
          Select Date
        </summary>
      </details>
    </div>
  </div>
</template>

<script setup>
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
