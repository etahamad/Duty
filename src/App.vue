<script setup lang="ts">

import Countdown from './components/Countdown.vue'
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
  </div>
</template>

<style scoped>
.quran {
  font-family: conv_original-hafs,'Traditional Arabic',tahoma, serif;
  font-size: 2em;
  width: 100%;
  text-align: center;
  margin: 2rem 0;
}
.quran span {
  display: block;
  overflow-wrap: break-word;
}
.quran .verses {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
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
@media (max-width: 768px) {
  .quran {
    font-size: 1.8em;
    padding: 0 1rem;
  }
}
</style>
