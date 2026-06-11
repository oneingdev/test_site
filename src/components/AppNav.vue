<template>
  <nav :class="{ scrolled: isScrolled }">
    <div class="nav-logo">오수지 <em>Suji Oh</em></div>

    <!-- 데스크탑 메뉴 -->
    <ul class="nav-links">
      <li><a href="#about" @click="closeMenu">About</a></li>
      <li><a href="#gallery" @click="closeMenu">Works</a></li>
      <li><a href="#exhibitions" @click="closeMenu">Exhibitions</a></li>
      <li><a href="#awards" @click="closeMenu">Awards</a></li>
      <li><a href="#contact" @click="closeMenu">Contact</a></li>
    </ul>

    <!-- 햄버거 버튼 (모바일) -->
    <button class="hamburger" @click="toggleMenu" :class="{ open: menuOpen }">
      <span></span>
      <span></span>
      <span></span>
    </button>

    <!-- 모바일 드로어 메뉴 -->
    <transition name="drawer">
      <div class="mobile-menu" v-if="menuOpen">
        <ul class="mobile-links">
          <li><a href="#about" @click="closeMenu">About</a></li>
          <li><a href="#gallery" @click="closeMenu">Works</a></li>
          <li><a href="#exhibitions" @click="closeMenu">Exhibitions</a></li>
          <li><a href="#awards" @click="closeMenu">Awards</a></li>
          <li><a href="#contact" @click="closeMenu">Contact</a></li>
        </ul>
      </div>
    </transition>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

defineProps({ artist: Object })

const isScrolled = ref(false)
const menuOpen = ref(false)

const handleScroll = () => { isScrolled.value = window.scrollY > 20 }
const toggleMenu = () => { menuOpen.value = !menuOpen.value }
const closeMenu = () => { menuOpen.value = false }

onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<style scoped>
nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 100;
  padding: 20px 48px;
  display: flex; justify-content: space-between; align-items: center;
  background: #ffffff;
  box-shadow: 0 1px 0 rgba(0,0,0,0.06);
  transition: padding 0.3s ease, box-shadow 0.3s ease;
}
nav.scrolled {
  padding: 14px 48px;
  box-shadow: 0 2px 16px rgba(0,0,0,0.08);
}

.nav-logo {
  font-family: 'Cormorant Garamond', serif;
  font-size: 20px; font-weight: 300;
  letter-spacing: 0.2em; color: var(--ink); text-transform: uppercase;
  z-index: 101;
}
.nav-logo em { font-style: italic; color: var(--gold); }

/* 데스크탑 링크 */
.nav-links { display: flex; gap: 32px; list-style: none; }
.nav-links a {
  font-size: 10px; letter-spacing: 0.25em; text-transform: uppercase;
  color: var(--ink); text-decoration: none; font-weight: 400;
  transition: color 0.3s; position: relative;
}
.nav-links a::after {
  content: ''; position: absolute;
  bottom: -2px; left: 0; right: 100%;
  height: 1px; background: var(--gold); transition: right 0.3s ease;
}
.nav-links a:hover::after { right: 0; }
.nav-links a:hover { color: var(--gold); }

/* 햄버거 버튼 */
.hamburger {
  display: none;
  flex-direction: column; justify-content: space-between;
  width: 24px; height: 16px;
  background: none; border: none; cursor: pointer; z-index: 101; padding: 0;
}
.hamburger span {
  display: block; width: 100%; height: 1px;
  background: var(--ink); transition: all 0.3s ease;
  transform-origin: center;
}
.hamburger.open span:nth-child(1) { transform: translateY(7.5px) rotate(45deg); }
.hamburger.open span:nth-child(2) { opacity: 0; }
.hamburger.open span:nth-child(3) { transform: translateY(-7.5px) rotate(-45deg); }

/* 모바일 드로어 */
.mobile-menu {
  position: fixed; top: 0; left: 0; right: 0; bottom: 0;
  background: #ffffff; z-index: 99;
  display: flex; align-items: center; justify-content: center;
}
.mobile-links {
  list-style: none; text-align: center;
  display: flex; flex-direction: column; gap: 40px;
}
.mobile-links a {
  font-family: 'Cormorant Garamond', serif;
  font-size: 36px; font-weight: 300; letter-spacing: 0.1em;
  color: var(--ink); text-decoration: none;
  transition: color 0.3s;
}
.mobile-links a:hover { color: var(--gold); }

/* 드로어 애니메이션 */
.drawer-enter-active, .drawer-leave-active { transition: opacity 0.3s ease; }
.drawer-enter-from, .drawer-leave-to { opacity: 0; }

/* 반응형 */
@media (max-width: 768px) {
  nav { padding: 18px 24px; }
  nav.scrolled { padding: 14px 24px; }
  .nav-links { display: none; }
  .hamburger { display: flex; }
}
</style>
