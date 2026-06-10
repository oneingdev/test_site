<template>
  <section id="about">
    <div class="section-header fade-in-up">
      <div class="section-num">01</div>
      <div>
        <div class="section-label">Artist Statement</div>
        <h2 class="section-title">작가 소개</h2>
      </div>
    </div>
    <div class="about-grid">
      <div class="about-portrait fade-in-up">
        <div class="portrait-frame">
          <div class="portrait-placeholder">작가 사진</div>
        </div>
        <!-- ✅ 오늘 기준 자동 계산된 경력 연차 표시 -->
        <div class="portrait-caption">{{ artist.name }} · Suji Oh · {{ careerYears }}년 활동</div>
      </div>
      <div class="about-content">
        <p class="about-text fade-in-up" v-html="artist.statement"></p>
        <p class="about-sub fade-in-up">{{ artist.bio }}</p>
        <div class="about-stats fade-in-up">
          <div v-for="stat in stats" :key="stat.label">
            <div class="stat-num">{{ stat.value }}</div>
            <div class="stat-label">{{ stat.label }}</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  artist: Object,
  stats: Array,
})

// ✅ 오늘 날짜 기준으로 경력 연차 자동 계산
const careerYears = computed(() => {
  return new Date().getFullYear() - props.artist.careerStartYear
})
</script>

<style scoped>
#about { background: var(--cream); }
.about-grid { display: grid; grid-template-columns: 1fr 2fr; gap: 80px; align-items: start; }

.portrait-frame {
  width: 100%; aspect-ratio: 3/4; background: var(--ink);
  position: relative; overflow: hidden;
}
.portrait-frame::before {
  content: ''; position: absolute; inset: -2px;
  border: 1px solid var(--gold); opacity: 0.5; z-index: 1;
}
.portrait-placeholder {
  width: 100%; height: 100%;
  display: flex; align-items: center; justify-content: center;
  font-family: 'Cormorant Garamond', serif; font-style: italic;
  color: rgba(255,255,255,0.2); font-size: 14px; letter-spacing: 0.15em;
}
.portrait-caption {
  margin-top: 16px; font-size: 10px; letter-spacing: 0.2em;
  text-transform: uppercase; color: var(--warm-gray); text-align: center;
}

.about-text {
  font-family: 'Cormorant Garamond', serif;
  font-size: 22px; font-weight: 300;
  line-height: 1.7; color: var(--ink); margin-bottom: 32px;
}
.about-text :deep(em) { font-style: italic; color: var(--gold); }
.about-sub {
  font-size: 12px; line-height: 1.9;
  color: var(--warm-gray); letter-spacing: 0.03em; margin-bottom: 48px;
}

.about-stats {
  display: grid; grid-template-columns: repeat(3, 1fr); gap: 32px;
  border-top: 1px solid var(--paper); padding-top: 32px;
}
.stat-num {
  font-family: 'Cormorant Garamond', serif;
  font-size: 48px; font-weight: 300; color: var(--gold); line-height: 1;
}
.stat-label {
  font-size: 10px; letter-spacing: 0.2em;
  text-transform: uppercase; color: var(--warm-gray); margin-top: 8px;
}
</style>
