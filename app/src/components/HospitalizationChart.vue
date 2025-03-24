<template>
  <div class="container flex justify-center flex-flow w-full">
    <Bar v-if="state.loaded && state.chartData" :data="state.chartData" />
    <div v-if="!state.loaded">Loading data...</div>
    <div v-if="state.error">{{ state.error }}</div>
  </div>
</template>

<script setup>
import { reactive, defineProps, onMounted } from 'vue'
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

const boroughHospitalizationCounts = {
  Bronx: 0,
  Brooklyn: 0,
  Manhattan: 0,
  Queens: 0,
  StatenIsland: 0,
}

const aggregateData = (data) => {
  const localBoroughHospitalizationCounts = { ...boroughHospitalizationCounts }

  data.forEach((item) => {
    localBoroughHospitalizationCounts.Bronx += parseInt(item.bx_hospitalized_count, 10) || 0
    localBoroughHospitalizationCounts.Brooklyn += parseInt(item.bk_hospitalized_count, 10) || 0
    localBoroughHospitalizationCounts.Manhattan += parseInt(item.mn_hospitalized_count, 10) || 0
    localBoroughHospitalizationCounts.Queens += parseInt(item.qn_hospitalized_count, 10) || 0
    localBoroughHospitalizationCounts.StatenIsland += parseInt(item.si_hospitalized_count, 10) || 0
  })

  const labels = Object.keys(localBoroughHospitalizationCounts)
  const hospitalizationCounts = Object.values(localBoroughHospitalizationCounts)

  return {
    labels: labels,
    datasets: [
      {
        label: 'Hospitalizations per Borough',
        data: hospitalizationCounts,
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
