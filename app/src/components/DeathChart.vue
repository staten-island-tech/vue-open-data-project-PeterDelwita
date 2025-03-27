<template>
  <div class="container flex justify-center flex-flow w-full">
    <Pie v-if="state.loaded && state.chartData" :data="state.chartData" />
    <div v-if="!state.loaded">Loading data...</div>
    <div v-if="state.error">{{ state.error }}</div>
  </div>
</template>

<script setup>
import { reactive, defineProps, onMounted } from 'vue'
import { Pie } from 'vue-chartjs'
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  ArcElement,
  CategoryScale,
  LinearScale,
} from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, ArcElement, CategoryScale, LinearScale)

const props = defineProps({
  apiUrl: {
    type: String,
    required: true,
  },
})

const state = reactive({
  loaded: false,
  chartData: null,
  error: null,
  allData: [],
})

const boroughDeathCounts = {
  Bronx: 0,
  Brooklyn: 0,
  Manhattan: 0,
  Queens: 0,
  StatenIsland: 0,
}

const aggregateData = (data) => {
  const localBoroughDeathCounts = { ...boroughDeathCounts }

  data.forEach((item) => {
    localBoroughDeathCounts.Bronx += parseInt(item.bx_death_count, 10) || 0
    localBoroughDeathCounts.Brooklyn += parseInt(item.bk_death_count, 10) || 0
    localBoroughDeathCounts.Manhattan += parseInt(item.mn_death_count, 10) || 0
    localBoroughDeathCounts.Queens += parseInt(item.qn_death_count, 10) || 0
    localBoroughDeathCounts.StatenIsland += parseInt(item.si_death_count, 10) || 0
  })

  const labels = Object.keys(localBoroughDeathCounts)
  const deathCounts = Object.values(localBoroughDeathCounts)

  return {
    labels: labels,
    datasets: [
      {
        label: 'Deaths per Borough',
        data: deathCounts,
        backgroundColor: ['#FF5733', '#33FF57', '#3357FF', '#FF33A8', '#FFD433'],
        borderColor: '#ffffff',
        borderWidth: 1,
      },
    ],
  }
}

const loadData = async () => {
  state.loaded = false
  state.error = null

  try {
    const response = await fetch(`${props.apiUrl}`)
    const data = await response.json()

    const aggregatedData = aggregateData(data)

    state.allData = aggregatedData
    state.chartData = state.allData

    state.loaded = true
  } catch (error) {
    state.error = error.message
    console.error(error)
  }
}

onMounted(() => {
  loadData()
})
</script>

<style scoped></style>
