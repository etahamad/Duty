<script setup lang="ts">

import Countdown from './components/Countdown.vue'
import EgyptHolidays from './components/EgyptHolidays.vue'
</script>

<template>
  <div id="app">
    <Countdown format="days" label="Days left:" />
    <Countdown format="months-days" label="Months and days left:" />
    <hr class="divider" />
    <EgyptHolidays />
  </div>
</template>

<style scoped>
.divider {
  border: none;
  border-top: 1px solid #ccc;
  margin: 20px 0;
}
</style>