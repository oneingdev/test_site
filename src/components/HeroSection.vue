<template>
  <section id="hero">
    <div class="hero-left">
      <div class="hero-label">시각예술가 · Visual Artist</div>
      <h1 class="hero-name">{{ artist.firstName }}<br><em>{{ artist.lastName }}</em></h1>
      <p class="hero-desc">{{ artist.tagline }}</p>
      <div class="hero-scroll">
        <div class="scroll-line"></div>
        Scroll to explore
      </div>
    </div>
    <div class="hero-right">
      <div class="hero-img-overlay"></div>
      <div class="hero-artwork">
        <div v-for="(tile, i) in heroTiles" :key="i" class="artwork-tile">
          <div class="tile-inner">
            <div class="tile-color" :class="'t' + (i + 1)">{{ tile }}</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
defineProps({
  artist: Object,
  heroTiles: Array,
})
</script>

<style scoped>
#hero {
  height: 100vh; display: grid; grid-template-columns: 1fr 1fr;
  position: relative; overflow: hidden;
  /* ✅ 흰색 nav 높이만큼 상단 여백 */
  padding-top: 0;
}
.hero-left {
  display: flex; flex-direction: column; justify-content: flex-end;
  padding: 80px 48px; background: var(--cream);
  position: relative; z-index: 2;
}
.hero-label {
  font-size: 10px; letter-spacing: 0.3em; text-transform: uppercase;
  color: var(--gold); margin-bottom: 24px;
}
.hero-name {
  font-family: 'Cormorant Garamond', serif;
  font-size: clamp(52px, 7vw, 96px); font-weight: 300;
  line-height: 0.95; letter-spacing: -0.02em; margin-bottom: 32px;
  animation: fadeUp 1.2s ease forwards;
}
.hero-name em { font-style: italic; color: var(--gold); }
.hero-desc {
  font-size: 12px; line-height: 1.8; color: var(--warm-gray);
  max-width: 320px; letter-spacing: 0.05em;
  animation: fadeUp 1.2s 0.2s ease forwards; opacity: 0;
}
.hero-scroll {
  margin-top: 48px; display: flex; align-items: center; gap: 16px;
  font-size: 10px; letter-spacing: 0.2em; text-transform: uppercase; color: var(--warm-gray);
  animation: fadeUp 1.2s 0.4s ease forwards; opacity: 0;
}
.scroll-line {
  width: 48px; height: 1px; background: var(--gold);
  animation: expandLine 1.5s 0.8s ease forwards;
  transform-origin: left; transform: scaleX(0);
}
.hero-right { background: var(--ink); position: relative; overflow: hidden; }
.hero-img-overlay {
  position: absolute; inset: 0;
  background: linear-gradient(135deg, rgba(184,147,63,0.15) 0%, transparent 60%); z-index: 1;
}
.hero-artwork {
  position: absolute; inset: 0;
  display: grid; grid-template-columns: 1fr 1fr; grid-template-rows: 1fr 1fr;
  gap: 2px; padding: 2px;
  animation: fadeIn 1.5s 0.3s ease forwards; opacity: 0;
}
.artwork-tile { overflow: hidden; }
.tile-inner { width: 100%; height: 100%; transition: transform 0.8s ease; }
.artwork-tile:hover .tile-inner { transform: scale(1.05); }
.tile-color {
  width: 100%; height: 100%;
  display: flex; align-items: center; justify-content: center;
  font-family: 'Cormorant Garamond', serif; font-style: italic;
  font-size: 14px; color: rgba(255,255,255,0.3); letter-spacing: 0.1em;
}
.t1 { background: linear-gradient(135deg, #2a2015, #4a3820); }
.t2 { background: linear-gradient(135deg, #1a1a2e, #2d2d44); }
.t3 { background: linear-gradient(135deg, #1e2a1e, #2a3d2a); }
.t4 { background: linear-gradient(135deg, #2a1a1a, #3d2a2a); }
</style>
