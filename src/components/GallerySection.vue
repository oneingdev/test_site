<template>
  <section id="gallery">
    <div class="section-header fade-in-up">
      <div class="section-num">02</div>
      <div>
        <div class="section-label">Portfolio</div>
        <h2 class="section-title">작품</h2>
      </div>
    </div>

    <div class="gallery-filter fade-in-up">
      <button
        v-for="cat in categories" :key="cat"
        class="filter-btn" :class="{ active: activeCategory === cat }"
        @click="activeCategory = cat">
        {{ cat }}
      </button>
    </div>

    <div class="gallery-masonry fade-in-up">
      <div
        v-for="work in filteredWorks" :key="work.id"
        class="gallery-item" @click="openModal(work)">
        <div class="gallery-item-inner">
          <div class="gallery-placeholder" :style="{ height: work.height + 'px', background: work.bg }">
            {{ work.title }}
          </div>
          <div class="gallery-overlay">
            <div class="gallery-work-title">{{ work.title }}</div>
            <div class="gallery-work-year">{{ work.year }} · {{ work.medium }}</div>
          </div>
        </div>
      </div>
    </div>

    <transition name="fade">
      <div class="modal-backdrop" v-if="modal.open" @click="modal.open = false">
        <button class="modal-close" @click="modal.open = false">✕ Close</button>
        <div class="modal-preview" :style="{ background: modal.work?.bg }">{{ modal.work?.title }}</div>
        <div class="modal-info" v-if="modal.work">
          <div class="modal-title">{{ modal.work.title }}</div>
          <div class="modal-year">{{ modal.work.year }} · {{ modal.work.medium }}</div>
        </div>
      </div>
    </transition>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'
const props = defineProps({ works: Array, categories: Array })
const activeCategory = ref('All')
const modal = ref({ open: false, work: null })
const filteredWorks = computed(() =>
  activeCategory.value === 'All'
    ? props.works
    : props.works.filter((w) => w.category === activeCategory.value)
)
const openModal = (work) => { modal.value = { open: true, work } }
</script>

<style scoped>
#gallery { background: var(--ink); color: var(--cream); }
#gallery .section-num { color: #2a2418; }
#gallery .section-title { color: var(--cream); }

.gallery-filter { display: flex; gap: 16px; margin-bottom: 48px; flex-wrap: wrap; }
.filter-btn {
  font-size: 10px; letter-spacing: 0.2em; text-transform: uppercase;
  background: none; border: 1px solid rgba(255,255,255,0.15);
  color: rgba(255,255,255,0.5); padding: 8px 20px; cursor: pointer; transition: all 0.3s;
}
.filter-btn.active, .filter-btn:hover {
  border-color: var(--gold); color: var(--gold); background: rgba(184,147,63,0.08);
}

.gallery-masonry { columns: 3; column-gap: 16px; }
.gallery-item { break-inside: avoid; margin-bottom: 16px; position: relative; overflow: hidden; cursor: pointer; }
.gallery-item-inner { position: relative; overflow: hidden; }
.gallery-placeholder {
  width: 100%; display: flex; align-items: center; justify-content: center;
  font-family: 'Cormorant Garamond', serif; font-style: italic;
  color: rgba(255,255,255,0.15); font-size: 13px; letter-spacing: 0.1em;
  transition: transform 0.6s ease;
}
.gallery-item:hover .gallery-placeholder { transform: scale(1.04); }
.gallery-overlay {
  position: absolute; inset: 0;
  background: linear-gradient(to top, rgba(10,8,5,0.9) 0%, transparent 50%);
  opacity: 0; transition: opacity 0.4s ease;
  display: flex; flex-direction: column; justify-content: flex-end; padding: 16px;
}
.gallery-item:hover .gallery-overlay { opacity: 1; }
.gallery-work-title {
  font-family: 'Cormorant Garamond', serif; font-size: 16px;
  font-style: italic; color: var(--cream); font-weight: 300;
}
.gallery-work-year { font-size: 10px; letter-spacing: 0.15em; color: var(--gold); margin-top: 4px; }

/* 모달 */
.modal-backdrop {
  position: fixed; inset: 0; background: rgba(10,8,5,0.95); z-index: 200;
  display: flex; align-items: center; justify-content: center; cursor: pointer;
}
.modal-close {
  position: absolute; top: 24px; right: 24px;
  font-size: 11px; letter-spacing: 0.25em; text-transform: uppercase;
  color: var(--warm-gray); cursor: pointer; background: none; border: none; transition: color 0.3s;
}
.modal-close:hover { color: var(--gold); }
.modal-preview {
  width: 80vw; height: 70vh; max-width: 900px; border-radius: 2px;
  display: flex; align-items: center; justify-content: center;
  font-family: 'Cormorant Garamond', serif; font-style: italic;
  color: rgba(255,255,255,0.2); font-size: 20px;
}
.modal-info { position: absolute; bottom: 32px; left: 24px; }
.modal-title {
  font-family: 'Cormorant Garamond', serif; font-size: 24px;
  font-style: italic; color: var(--cream); font-weight: 300;
}
.modal-year { font-size: 11px; letter-spacing: 0.2em; color: var(--gold); margin-top: 4px; }

.fade-enter-active, .fade-leave-active { transition: opacity 0.3s; }
.fade-enter-from, .fade-leave-to { opacity: 0; }

/* 태블릿 */
@media (max-width: 1024px) {
  .gallery-masonry { columns: 2; }
}

/* 모바일 */
@media (max-width: 768px) {
  #gallery { padding: 80px 24px; }
  .gallery-masonry { columns: 2; column-gap: 10px; }
  .gallery-item { margin-bottom: 10px; }
  .modal-preview { width: 92vw; height: 60vw; }
  .modal-info { bottom: 20px; left: 16px; }
  .modal-title { font-size: 18px; }
}

@media (max-width: 480px) {
  .gallery-masonry { columns: 1; }
}
</style>
