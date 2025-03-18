<template>
  <router-link :to="dayPath">
    <h2>{{ date.date_of_interest }}</h2>
  </router-link>
  <!--Good place to put router-link-->
</template>

<script setup>
import { Chart } from 'chart.js/auto'
import { computed } from 'vue'

const props = defineProps({
  date: Object,
}) // Should represent a day and the API is huge. Therefore each component needs its own separate URL. Therefore, we have to go into the router file and update it to accommodate these components.
// Since I want to use this component to represent each individual day, I therefore want to make a separate .vue file in the view folder, update the router file accordingly, and make a dropdown (use v-for on names) from which the user will access each day.
const dayPath = computed(() => {
  return `/day/${props.date}`
})
</script>

<style scoped></style>
