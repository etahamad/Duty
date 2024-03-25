<template>
  <div>
    <div v-if="nextHoliday">
      Next holiday: {{ nextHoliday.date }} - {{ nextHoliday.localName }}
      <br>
      Days left for the next holiday: {{ daysLeft }} days
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, computed } from 'vue'
import axios from 'axios'

interface Holiday {
  date: string;
  localName: string;
}

const nextHoliday = ref<Holiday | null>(null)


const daysLeft = computed(() => {
  if (nextHoliday.value) {
    const currentDate = new Date()
    const nextHolidayDate = new Date(nextHoliday.value.date)
    const diffInTime = nextHolidayDate.getTime() - currentDate.getTime()
    return Math.ceil(diffInTime / (1000 * 3600 * 24))
  }
  return null
})

onMounted(async () => {
  const response = await axios.get('https://date.nager.at/api/v3/NextPublicHolidays/EG')
  nextHoliday.value = response.data[0] || null
})
</script>