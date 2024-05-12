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

interface Holiday {
  date: string;
  localName: string;
}

const nextHoliday = ref<Holiday | null>(null)

const holidays: Holiday[] = [
  { "date": "2024-01-07", "localName": "Coptic Christmas Day" },
  { "date": "2024-01-25", "localName": "January 25th Revolution and National Police Day" },
  { "date": "2024-04-09", "localName": "Eid Al-Fitr" },
  { "date": "2024-04-10", "localName": "Eid Al-Fitr" },
  { "date": "2024-04-11", "localName": "Eid Al-Fitr" },
  { "date": "2024-04-12", "localName": "Eid Al-Fitr" },
  { "date": "2024-04-13", "localName": "Eid Al-Fitr" },
  { "date": "2024-04-14", "localName": "Eid Al-Fitr" },
  { "date": "2024-04-25", "localName": "Sinai Liberation Day (April 25, 1982)" },
  { "date": "2024-05-05", "localName": "Labor Day" },
  { "date": "2024-05-06", "localName": "Sham El-Nessim" },
  { "date": "2024-06-16", "localName": "Arafat's Day" },
  { "date": "2024-06-17", "localName": "Eid Al-Adha" },
  { "date": "2024-06-18", "localName": "Eid Al-Adha" },
  { "date": "2024-06-19", "localName": "Eid Al-Adha" },
  { "date": "2024-06-20", "localName": "Eid Al-Adha" },
  { "date": "2024-06-30", "localName": "June 30 Revolution" },
  { "date": "2024-07-08", "localName": "Islamic New Year" },
  { "date": "2024-07-23", "localName": "The July 23 Revolution Day (July 23, 1952)" },
  { "date": "2024-09-16", "localName": "Prophet Muhammad's Birthday (Mawlid Al-Nabi)" },
  { "date": "2024-10-06", "localName": "Armed Forces Day (October 6, 1973)" }
]

const daysLeft = computed(() => {
  if (nextHoliday.value) {
    const currentDate = new Date()
    const nextHolidayDate = new Date(nextHoliday.value.date)
    const diffInTime = nextHolidayDate.getTime() - currentDate.getTime()
    return Math.ceil(diffInTime / (1000 * 3600 * 24))
  }
  return null
})

onMounted(() => {
  const currentDate = new Date()
  for (let holiday of holidays) {
    const holidayDate = new Date(holiday.date)
    if (holidayDate > currentDate) {
      nextHoliday.value = holiday
      break
    }
  }
})
</script>