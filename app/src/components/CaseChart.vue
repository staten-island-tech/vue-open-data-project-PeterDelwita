<template>
  <div class="container flex justify-center flex-flow w-full">
    <Doughnut v-if="state.loaded && state.chartData" :data="state.chartData" />
    <div v-if="!state.loaded">Loading data...</div>
    <div v-if="state.error">{{ state.error }}</div>
  </div>
</template>

<script setup>
import { reactive, defineProps, onMounted } from 'vue'
import { Doughnut } from 'vue-chartjs'
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
})

const boroughCaseCounts = {
  Bronx: 0,
  Brooklyn: 0,
  Manhattan: 0,
  Queens: 0,
  StatenIsland: 0,
}

const aggregateData = (data) => {
  const localBoroughCaseCounts = { ...boroughCaseCounts }

  data.forEach((item) => {
    localBoroughCaseCounts.Bronx += parseInt(item.bx_case_count, 10) || 0
    localBoroughCaseCounts.Brooklyn += parseInt(item.bk_case_count, 10) || 0
    localBoroughCaseCounts.Manhattan += parseInt(item.mn_case_count, 10) || 0
    localBoroughCaseCounts.Queens += parseInt(item.qn_case_count, 10) || 0
    localBoroughCaseCounts.StatenIsland += parseInt(item.si_case_count, 10) || 0
  })

  const labels = Object.keys(localBoroughCaseCounts)
  const caseCounts = Object.values(localBoroughCaseCounts)

  return {
    labels: labels,
    datasets: [
      {
        label: 'Cases per Borough',
        data: caseCounts,
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
    const response = await fetch(props.apiUrl)
    const data = await response.json()

    const aggregatedData = aggregateData(data)

    state.chartData = aggregatedData
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
