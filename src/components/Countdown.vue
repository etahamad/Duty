<template>
  <div class="countdown-container">
    <div v-if="isCountdownOver" class="completion-message">
      <h4>🎉 Alhamdulillah الحمد لله 🎉</h4>
      <p>All praise is due to Allah</p>
      <p>Military service is finally over! 🪖</p>
    </div>
    <div v-else>
      <h4>{{ label }} {{ formattedCountdown }}</h4>
      <div class="progress-wrapper" @click="handleClick">
        <ProgressBar 
          :value="Number(percentageDone)" 
          :showValue="true" 
          :displayValueTemplate="valueTemplate" 
          :style="{
            height: '20px',
            width: '450px',
            margin: '0 auto',
            cursor: 'pointer'
          }" 
        />
      </div>
      <div v-if="showEasterEgg" class="easter-egg">
        <p>{{ currentMessage.arabic }}</p>
        <p>{{ currentMessage.english }}</p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted, computed } from 'vue'
import ProgressBar from 'primevue/progressbar';

const messages = [
  {
    arabic: "🫡 صبر جميل والله المستعان",
    english: "Beautiful patience, and Allah is the one sought for help"
  },
  {
    arabic: "✨ اللهم اجعل لنا من كل ضيق مخرجا",
    english: "O Allah, make for us a way out of every difficulty"
  },
  {
    arabic: "🌟 مع الصبر يأتي الفرج",
    english: "With patience comes relief"
  },
  {
    arabic: "💫 كل شيء بقدر",
    english: "Everything happens by divine decree"
  },
  {
    arabic: "🤲 الحمد لله على كل حال",
    english: "Praise be to Allah in all circumstances"
  }
]

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
const targetDate = new Date('2025-02-10T00:00:00')
const totalDaysBetween = Math.floor((targetDate.getTime() - startDate.getTime()) / (1000 * 60 * 60 * 24))
let totalDays = ref(totalDaysBetween)

let intervalId: number | undefined

const isCountdownOver = ref(false)
const showEasterEgg = ref(false)
const clickCount = ref(0)
const currentMessage = ref(messages[0])

onMounted(() => {
  intervalId = setInterval(() => {
    const now = new Date()
    const diff = targetDate.getTime() - now.getTime()

    if (diff > 0) {
      totalDays.value = Math.floor(diff / (1000 * 60 * 60 * 24))
    } else {
      isCountdownOver.value = true
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
    const now = new Date();
    let years = targetDate.getFullYear() - now.getFullYear();
    let months;
    let days;

    months = targetDate.getMonth() - now.getMonth();
    if (months < 0) {
      months += 12;
      years--;
    }

    days = targetDate.getDate() - now.getDate();
    if (days < 0) {
      months--;
      let nowLastMonth = new Date(now.getFullYear(), now.getMonth(), 0);
      days += nowLastMonth.getDate();
    }

    return `${months} months, ${days} days`;
  } else {
    return `${totalDays.value} days`;
  }
});

const percentageDone = computed(() => {
  return ((totalDaysBetween - totalDays.value) / totalDaysBetween * 100).toFixed(0)
})

const valueTemplate = (value: number) => `${value}`;

const handleClick = () => {
  clickCount.value++
  if (clickCount.value >= 3) {
    // Get random message
    const randomIndex = Math.floor(Math.random() * messages.length)
    currentMessage.value = messages[randomIndex]
    showEasterEgg.value = true
    
    setTimeout(() => {
      showEasterEgg.value = false
      clickCount.value = 0
    }, 3000)
  }
}
</script>

<style scoped>
.countdown-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

.completion-message {
  text-align: center;
}

.completion-message h4 {
  font-size: 1.5em;
  margin-bottom: 0.5rem;
}

.completion-message p {
  margin: 0.5rem 0;
  color: #666;
}

.progress-wrapper {
  width: 100%;
  display: flex;
  justify-content: center;
}

@media (max-width: 768px) {
  .progress-wrapper :deep(.p-progressbar) {
    width: 300px !important;
  }
}

.easter-egg {
  margin-top: 1rem;
  font-size: 0.9em;
  color: #666;
  animation: fadeIn 0.5s ease-in;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
</style>
