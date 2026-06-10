<template>
  <nav :class="{ scrolled: isScrolled }">
    <div class="nav-logo">오수지 <em>Suji Oh</em></div>
    <ul class="nav-links">
      <li><a href="#about">About</a></li>
      <li><a href="#gallery">Works</a></li>
      <li><a href="#exhibitions">Exhibitions</a></li>
      <li><a href="#awards">Awards</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

defineProps({
  artist: Object,
})

// ✅ 스크롤 여부 감지 → 배경 전환
const isScrolled = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 20
}

onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<style scoped>
nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 100;
  padding: 24px 48px;
  display: flex; justify-content: space-between; align-items: center;
  /* ✅ 항상 흰색 배경 고정, 글자색 어둡게 고정 */
  background: #ffffff;
  box-shadow: 0 1px 0 rgba(0, 0, 0, 0.06);
  transition: padding 0.3s ease, box-shadow 0.3s ease;
}

/* 스크롤 시 약간 컴팩트하게 */
nav.scrolled {
  padding: 16px 48px;
  box-shadow: 0 2px 16px rgba(0, 0, 0, 0.08);
}

.nav-logo {
  font-family: 'Cormorant Garamond', serif;
  font-size: 22px; font-weight: 300;
  letter-spacing: 0.2em;
  color: var(--ink);
  text-transform: uppercase;
}
.nav-logo em {
  font-style: italic;
  color: var(--gold);
}

.nav-links { display: flex; gap: 36px; list-style: none; }

.nav-links a {
  font-size: 10px; letter-spacing: 0.25em; text-transform: uppercase;
  color: var(--ink); /* 항상 어두운 색 */
  text-decoration: none; font-weight: 400;
  transition: color 0.3s; position: relative;
}
.nav-links a::after {
  content: ''; position: absolute;
  bottom: -2px; left: 0; right: 100%;
  height: 1px; background: var(--gold);
  transition: right 0.3s ease;
}
.nav-links a:hover::after { right: 0; }
.nav-links a:hover { color: var(--gold); }
</style>
