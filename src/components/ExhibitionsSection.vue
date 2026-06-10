<template>
  <section id="exhibitions">
    <div class="section-header fade-in-up">
      <div class="section-num">03</div>
      <div>
        <div class="section-label">Exhibition History</div>
        <h2 class="section-title">전시 이력</h2>
      </div>
    </div>

    <!-- ✅ exhibitions 배열 길이가 자동으로 카운트에 반영됨 -->
    <div class="ex-count fade-in-up">총 {{ exhibitions.length }}회 전시</div>

    <div class="exhibitions-list">
      <div v-for="ex in exhibitions" :key="ex.id" class="exhibition-item fade-in-up">
        <div class="ex-year">{{ ex.year }}</div>
        <div class="ex-content">
          <div class="ex-title">{{ ex.title }}</div>
          <div class="ex-venue">{{ ex.venue }} · {{ ex.location }}</div>
          <span class="ex-type">{{ ex.type }}</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
defineProps({
  exhibitions: Array,
})
</script>

<style scoped>
#exhibitions { background: var(--paper); }

.ex-count {
  font-size: 11px; letter-spacing: 0.2em; text-transform: uppercase;
  color: var(--warm-gray); margin-bottom: 40px; margin-top: -48px;
}

.exhibitions-list { max-width: 800px; }
.exhibition-item {
  display: grid; grid-template-columns: 80px 1fr; gap: 32px;
  padding: 36px 0; border-bottom: 1px solid rgba(26,22,18,0.1);
  position: relative; transition: all 0.3s;
}
.exhibition-item::before {
  content: ''; position: absolute;
  left: -48px; top: 0; bottom: 0; width: 2px;
  background: var(--gold); transform: scaleY(0);
  transition: transform 0.3s ease; transform-origin: top;
}
.exhibition-item:hover::before { transform: scaleY(1); }
.exhibition-item:hover { padding-left: 16px; }

.ex-year {
  font-family: 'Cormorant Garamond', serif;
  font-size: 28px; font-weight: 300; color: var(--gold); line-height: 1; padding-top: 4px;
}
.ex-title { font-family: 'Cormorant Garamond', serif; font-size: 22px; font-weight: 300; margin-bottom: 6px; }
.ex-venue {
  font-size: 11px; letter-spacing: 0.15em; text-transform: uppercase;
  color: var(--warm-gray); margin-bottom: 8px;
}
.ex-type {
  display: inline-block; font-size: 9px; letter-spacing: 0.2em; text-transform: uppercase;
  border: 1px solid var(--gold); color: var(--gold); padding: 3px 10px;
}
</style>
