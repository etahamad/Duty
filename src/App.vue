<script setup lang="ts">

import Countdown from './components/Countdown.vue'
import EgyptHolidays from './components/EgyptHolidays.vue'
</script>

<template>
  <div id="app">
    <a href="https://github.com/etahamad/DutyFree" target="_blank" class="github-link">
      <i class="fab fa-github"></i>
      <span>View on GitHub</span>
    </a>
    <h3 class="quran">وَأَن لَّيْسَ لِلْإِنسَانِ إِلَّا مَا سَعَىٰ (39) وَأَنَّ سَعْيَهُ سَوْفَ يُرَىٰ (40)﴾ [ سورة النجم ]﴿</h3>
    <Countdown format="months-days" label="Months and days left:" />
    <hr class="divider" />
    <EgyptHolidays />
  </div>
</template>

<style scoped>
.quran {
  font-family: conv_original-hafs,'Traditional Arabic',tahoma, serif;
  font-size: 1.44em;
}
.divider {
  border: none;
  border-top: 1px solid #ccc;
  margin: 20px 0;
}
.github-link {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-decoration: none;
  color: inherit;
}
.github-link span {
  margin-top: 5px;
}
.fab {
  font-size: 24px;
  color: #000;
}
</style>
