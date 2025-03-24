<script setup>
import { RouterLink, RouterView } from 'vue-router'

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
    COVID-19 Counts of Cases, Hospitalizations, and Deaths
  </h1>
  <div class="button-container bg-gray-200 flex justify-center flex-wrap w=full">
    <nav>
      <RouterLink to="/cases">
        <button
          class="btn text-[24px] p-2 m-2 rounded-lg border-red-600 border-solid border-2 bg-white text-red-600 hover:bg-gray-950 hover:text-red-500 hover:border-red-600 hover:shadow-red-600/90"
        >
          Cases
        </button>
      </RouterLink>

      <RouterLink to="/deaths">
        <button
          class="btn text-[24px] p-2 m-2 rounded-lg border-red-600 border-solid border-2 bg-white text-red-600 hover:bg-gray-950 hover:text-red-500 hover:border-red-600 hover:shadow-red-600/90"
        >
          Deaths
        </button>
      </RouterLink>

      <RouterLink to="/hospitalizations">
        <button
          class="btn text-[24px] p-2 m-2 rounded-lg border-red-600 border-solid border-2 bg-white text-red-600 hover:bg-gray-950 hover:text-red-500 hover:border-red-600 hover:shadow-red-600/90"
        >
          Hospitalizations
        </button>
      </RouterLink>
    </nav>
  </div>

  <RouterView />
  <!--You need this to go to different pages-->
</template>

<style scoped></style>
