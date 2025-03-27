<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <main class="bg-gray-100">
    <!--API: https://data.cityofnewyork.us/resource/rc75-m7u3.json -->
    <h1 class="text-red-500 text-center text-[64px] font-bold">
      COVID-19 Counts of Cases, Hospitalizations, and Deaths
    </h1>
    <div class="button-container bg-gray-300 flex justify-center flex-wrap w-full">
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
  </main>
</template>

<style scoped></style>
