<template>
  <section id="awards">
    <div class="section-header fade-in-up">
      <div class="section-num">04</div>
      <div>
        <div class="section-label">Recognition</div>
        <h2 class="section-title">수상 이력</h2>
      </div>
    </div>

    <div class="awards-count fade-in-up">총 {{ awards.length }}개 수상</div>

    <div class="awards-list">
      <div v-for="award in awards" :key="award.year + award.title" class="award-item fade-in-up">
        <div class="award-year">{{ award.year }}</div>
        <div class="award-content">
          <div class="award-title">{{ award.title }}</div>
          <div class="award-org">{{ award.org }}</div>
        </div>
        <!-- 트로피 아이콘 -->
        <div class="award-icon">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
            <path d="M6 9H4a2 2 0 0 1-2-2V5h4"/>
            <path d="M18 9h2a2 2 0 0 0 2-2V5h-4"/>
            <path d="M12 17v4"/>
            <path d="M8 21h8"/>
            <path d="M6 3h12v8a6 6 0 0 1-12 0V3z"/>
          </svg>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
defineProps({
  awards: Array,
})
</script>

<style scoped>
#awards { background: var(--ink); color: var(--cream); }
#awards .section-num { color: #2a2418; }
#awards .section-title { color: var(--cream); }

.awards-count {
  font-size: 11px; letter-spacing: 0.2em; text-transform: uppercase;
  color: var(--warm-gray); margin-bottom: 40px; margin-top: -48px;
}

.awards-list { max-width: 800px; }

.award-item {
  display: grid;
  grid-template-columns: 80px 1fr 40px;
  gap: 32px;
  padding: 28px 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
  align-items: center;
  position: relative;
  transition: all 0.3s;
}
.award-item::before {
  content: '';
  position: absolute;
  left: -48px; top: 0; bottom: 0; width: 2px;
  background: var(--gold);
  transform: scaleY(0);
  transition: transform 0.3s ease;
  transform-origin: top;
}
.award-item:hover::before { transform: scaleY(1); }
.award-item:hover { padding-left: 16px; }
.award-item:hover .award-icon { color: var(--gold); }

.award-year {
  font-family: 'Cormorant Garamond', serif;
  font-size: 24px; font-weight: 300;
  color: var(--gold); line-height: 1;
}

.award-title {
  font-family: 'Cormorant Garamond', serif;
  font-size: 20px; font-weight: 300;
  color: var(--cream); margin-bottom: 4px;
}
.award-org {
  font-size: 10px; letter-spacing: 0.15em;
  text-transform: uppercase; color: var(--warm-gray);
}

.award-icon {
  color: rgba(255, 255, 255, 0.15);
  transition: color 0.3s;
  display: flex; align-items: center; justify-content: flex-end;
}
</style>
