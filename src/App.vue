<template>
  <div id="app">
    <div class="cursor" :style="{ left: cursor.x + 'px', top: cursor.y + 'px' }"></div>
    <div class="cursor-ring" :style="{ left: cursor.x + 'px', top: cursor.y + 'px' }"></div>

    <AppNav :artist="artist" />
    <HeroSection :artist="artist" :heroTiles="heroTiles" />
    <AboutSection :artist="artist" :stats="stats" />
    <GallerySection :works="works" :categories="categories" />
    <ExhibitionsSection :exhibitions="exhibitions" />
    <AwardsSection :awards="awards" />
    <ContactSection :contactLinks="contactLinks" />

    <footer class="site-footer">
      <span>© 2024 오수지 · Suji Oh. All rights reserved.</span>
      <span>Seoul, Korea</span>
    </footer>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import AppNav from './components/AppNav.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import GallerySection from './components/GallerySection.vue'
import ExhibitionsSection from './components/ExhibitionsSection.vue'
import AwardsSection from './components/AwardsSection.vue'
import ContactSection from './components/ContactSection.vue'

// ─── 커서 ───────────────────────────────────────────
const cursor = ref({ x: 0, y: 0 })

// ─── 작가 기본 정보 ──────────────────────────────────
const artist = {
  name: '오수지',
  firstName: 'Suji',
  lastName: 'Oh',
  careerStartYear: 2012, // ✅ 경력 시작 연도만 입력하면 연차 자동 계산
  tagline: '빛과 색채를 통해 감정의 언어를 탐구하는 시각예술가. 캔버스 위에서 현실과 내면의 경계를 지웁니다.',
  statement: '나의 작업은 <em>기억과 망각</em> 사이에 존재합니다. 색은 언어가 닿지 못하는 곳에서 말을 걸어옵니다.',
  bio: '서울을 기반으로 활동하는 시각예술가로, 회화와 설치를 중심으로 인간의 감정과 공간의 관계를 탐구합니다. 홍익대학교 회화과를 졸업하고 파리 국립 고등 미술학교에서 수학하였으며, 국내외 다수의 전시에 참여하였습니다.',
}

// ─── 수상 이력 배열 ──────────────────────────────────
// ✅ 항목을 추가하면 Awards 수가 자동으로 반영됨
const awards = [
  { year: 2023, title: '올해의 작가상', org: '한국현대미술협회' },
  { year: 2022, title: 'Asia Pacific Art Prize', org: 'APF Foundation' },
  { year: 2021, title: '신진작가 지원상', org: '서울문화재단' },
  { year: 2020, title: 'Emerging Artist Award', org: 'Saatchi Gallery' },
  { year: 2018, title: '우수작품상', org: '국립현대미술관' },
  { year: 2016, title: '청년작가상', org: '갤러리 현대' },
  { year: 2015, title: '졸업작품 최우수상', org: '홍익대학교' },
  { year: 2014, title: 'Prix de la Création', org: 'École nationale supérieure des Beaux-Arts' },
]

// ─── 전시 이력 배열 ──────────────────────────────────
// ✅ 항목을 추가하면 Exhibitions 수가 자동으로 반영됨
const exhibitions = [
  { id: 1,  year: 2024, title: '그림자의 무게 — Weight of Shadows', venue: '아트선재센터', location: 'Seoul', type: '개인전' },
  { id: 2,  year: 2023, title: 'Pulse: 동아시아 현대미술', venue: 'Museum of Contemporary Art', location: 'Tokyo', type: '그룹전' },
  { id: 3,  year: 2023, title: '시선의 여백', venue: '갤러리 현대', location: 'Seoul', type: '그룹전' },
  { id: 4,  year: 2022, title: 'Silent Geometries', venue: 'Palais de Tokyo', location: 'Paris', type: '그룹전' },
  { id: 5,  year: 2021, title: '안과 밖 — Inside Out', venue: '국립현대미술관', location: 'Seoul', type: '개인전' },
  { id: 6,  year: 2020, title: 'Emerging Voices', venue: 'Saatchi Gallery', location: 'London', type: '그룹전' },
  { id: 7,  year: 2019, title: '색채의 언어', venue: '대림미술관', location: 'Seoul', type: '그룹전' },
  { id: 8,  year: 2018, title: 'Between Lines', venue: 'Gallery Side 2', location: 'Tokyo', type: '그룹전' },
  { id: 9,  year: 2017, title: '잔상 — Afterimage', venue: '아르코미술관', location: 'Seoul', type: '개인전' },
  { id: 10, year: 2016, title: 'New Visions', venue: 'Tate Modern', location: 'London', type: '그룹전' },
]

// ─── 작품 목록 ───────────────────────────────────────
const works = [
  { id: 1, title: 'Untitled No.1',      year: 2024, medium: '캔버스에 유채',   category: '회화', height: 280, bg: 'linear-gradient(135deg, #2a1a2e, #4a2d4a)' },
  { id: 2, title: 'Fragment of Blue',   year: 2024, medium: '캔버스에 아크릴', category: '회화', height: 200, bg: 'linear-gradient(135deg, #1a2a3a, #2d4a5a)' },
  { id: 3, title: 'Echo Chamber',       year: 2023, medium: '혼합매체 설치',   category: '설치', height: 240, bg: 'linear-gradient(135deg, #1a2a1a, #2d4a2d)' },
  { id: 4, title: 'Before the Silence', year: 2023, medium: '종이에 연필',     category: '드로잉', height: 180, bg: 'linear-gradient(135deg, #2a2a1a, #3d3d2a)' },
  { id: 5, title: 'Residue',            year: 2022, medium: '캔버스에 유채',   category: '회화', height: 320, bg: 'linear-gradient(135deg, #2a1a1a, #4a2a2a)' },
  { id: 6, title: 'Threshold',          year: 2022, medium: '혼합매체 설치',   category: '설치', height: 200, bg: 'linear-gradient(135deg, #1a1a2a, #2a2a4a)' },
]

const categories = ['All', '회화', '설치', '드로잉']

// ─── About 통계 (자동 계산) ───────────────────────────
// ✅ careerStartYear, exhibitions 배열, awards 배열로 자동 계산
const stats = computed(() => {
  const yearsOfWork = new Date().getFullYear() - artist.careerStartYear
  return [
    { value: `${yearsOfWork}+`, label: 'Years of Work' },
    { value: exhibitions.length,  label: 'Exhibitions' },
    { value: awards.length,       label: 'Awards' },
  ]
})

// ─── 연락처 ──────────────────────────────────────────
// ✅ Studio 제거, Email + Instagram만
const contactLinks = [
  {
    label: 'Email',
    value: 'hello@sujioh.com',       // ✏️ 실제 이메일로 변경하세요
    href: 'mailto:hello@sujioh.com',
    icon: null,
  },
  {
    label: 'Instagram',
    value: '@suji.oh',               // ✏️ 실제 인스타 계정으로 변경하세요
    href: 'https://instagram.com/suji.oh',
    icon: 'instagram',
  },
]

const heroTiles = ['Untitled I', 'Fragment', 'Echo', 'Silence']

onMounted(() => {
  document.addEventListener('mousemove', (e) => {
    cursor.value = { x: e.clientX, y: e.clientY }
  })
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) entry.target.classList.add('visible')
    })
  }, { threshold: 0.1 })
  document.querySelectorAll('.fade-in-up').forEach((el) => observer.observe(el))
})
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;1,300;1,400&family=Montserrat:wght@300;400;500&display=swap');

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

:root {
  --cream: #f5f0e8;
  --ink: #1a1612;
  --warm-gray: #8a847c;
  --gold: #b8933f;
  --gold-light: #d4ad5f;
  --paper: #ede8de;
  --dark-ink: #0e0c0a;
}

html { scroll-behavior: smooth; }
body {
  font-family: 'Montserrat', sans-serif;
  background: var(--cream);
  color: var(--ink);
  overflow-x: hidden;
  cursor: none;
}

.cursor {
  position: fixed; width: 8px; height: 8px;
  background: var(--gold); border-radius: 50%;
  pointer-events: none; z-index: 9999;
  transform: translate(-50%, -50%);
}
.cursor-ring {
  position: fixed; width: 32px; height: 32px;
  border: 1px solid var(--gold); border-radius: 50%;
  pointer-events: none; z-index: 9998;
  transform: translate(-50%, -50%);
  transition: all 0.2s ease; opacity: 0.6;
}

.fade-in-up {
  opacity: 0; transform: translateY(24px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}
.fade-in-up.visible { opacity: 1; transform: translateY(0); }

section { padding: 120px 48px; }

.section-header { display: flex; align-items: center; gap: 24px; margin-bottom: 72px; }
.section-num {
  font-family: 'Cormorant Garamond', serif;
  font-size: 72px; font-weight: 300;
  color: var(--paper); line-height: 1; user-select: none;
}
.section-label {
  font-size: 9px; letter-spacing: 0.35em;
  text-transform: uppercase; color: var(--gold); margin-bottom: 6px;
}
.section-title {
  font-family: 'Cormorant Garamond', serif;
  font-size: 42px; font-weight: 300; line-height: 1.1;
}

.site-footer {
  background: var(--dark-ink);
  border-top: 1px solid rgba(255,255,255,0.05);
  padding: 32px 48px;
  display: flex; justify-content: space-between; align-items: center;
  color: var(--warm-gray); font-size: 10px; letter-spacing: 0.15em;
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(30px); }
  to   { opacity: 1; transform: translateY(0); }
}
@keyframes fadeIn {
  from { opacity: 0; } to { opacity: 1; }
}
@keyframes expandLine {
  from { transform: scaleX(0); } to { transform: scaleX(1); }
}
</style>
