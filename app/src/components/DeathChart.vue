<template>
  <div class="container">
    <Bar v-if="loaded" :data="chartData"></Bar>
  </div>
</template>

<script setup>
import { reactive } from 'vue'
import { Bar } from 'vue-chartjs'
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
} from 'chart.js'
ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

export default {
  name: 'BarChart',
  component: { Bar },
  data: () => ({
    loaded: false,
    chartData: null,
  }),
  async mounted() {
    this.loaded = false

    try {
      const response = await fetch('https://data.cityofnewyork.us/resource/rc75-m7u3.json')
      const { deathChart } = await response.json()
      this.chartData = {
        labels: deathChart.map((item) => item.day),
        datasets: [
          {
            label: 'Death Count,',
            data: deathChart.map((item) => item.deaths),
            borderWidth: 1,
          },
        ],
      }
      this.loaded = true
    } catch (error) {
      console.error(error)
    }
  },
}
</script>

<style scoped></style>
