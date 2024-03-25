<template>
  <div>
    <p>{{ label }} {{ formattedCountdown }}</p>
    <ProgressBar :value="Number(percentageDone)" :showValue="true" :displayValueTemplate="valueTemplate" :style="{height: '20px'}" />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted, computed } from 'vue'
import ProgressBar from 'primevue/progressbar';

const props = defineProps({
  format: {
    type: String,
    default: 'days'
  },
  label: {
    type: String,
    default: 'Countdown:'
  }
})

const startDate = new Date('2024-02-25T00:00:00')
const targetDate = new Date('2025-02-25T00:00:00')
const totalDaysBetween = Math.floor((targetDate.getTime() - startDate.getTime()) / (1000 * 60 * 60 * 24))
let totalDays = ref(totalDaysBetween)

let intervalId: number | undefined

onMounted(() => {
  intervalId = setInterval(() => {
    const now = new Date()
    const diff = targetDate.getTime() - now.getTime()

    if (diff > 0) {
      totalDays.value = Math.floor(diff / (1000 * 60 * 60 * 24))
    } else {
      clearInterval(intervalId)
    }
  }, 1000)
})

onUnmounted(() => {
  if (intervalId) {
    clearInterval(intervalId)
  }
})

const formattedCountdown = computed(() => {
  if (props.format === 'months-days') {
    const months = Math.floor(totalDays.value / 30)
    const days = totalDays.value % 30
    return `${months} months, ${days} days`
  } else {
    return `${totalDays.value} days`
  }
})

const percentageDone = computed(() => {
  return ((totalDaysBetween - totalDays.value) / totalDaysBetween * 100).toFixed(0)
})

const valueTemplate = (value: number) => `${value}`;
</script>