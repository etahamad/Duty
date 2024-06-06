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
    <h3 class="quran">
      <div class="verses">
        <span>وَأَن لَّيْسَ لِلْإِنسَانِ إِلَّا مَا سَعَىٰ (39)</span>
        <span>وَأَنَّ سَعْيَهُ سَوْفَ يُرَىٰ (40) [سورة النجم]</span>
      </div>
    </h3>
    <Countdown format="months-days" label="Time left:" />
    <hr class="divider" />
    <EgyptHolidays />
  </div>
</template>

<style scoped>
.quran {
  font-family: conv_original-hafs,'Traditional Arabic',tahoma, serif;
  font-size: 1.2em; /* Adjust the font size here */
  width: 100%; /* Ensure the container takes the full width */
  text-align: center; /* Center the text */
}
.quran span {
  display: block;
  overflow-wrap: break-word; /* Break the word if it's too long */
}
.quran .verses {
  display: flex;
  flex-direction: column;
  align-items: center;
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
