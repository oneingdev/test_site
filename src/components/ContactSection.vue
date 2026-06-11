<template>
  <section id="contact">
    <div class="section-header fade-in-up">
      <div class="section-num">05</div>
      <div>
        <div class="section-label">Get in Touch</div>
        <h2 class="section-title">연락처</h2>
      </div>
    </div>

    <div class="contact-grid">
      <div>
        <p class="contact-tagline fade-in-up">
          작품 구입 및 전시 <em>협업</em> 문의는<br>언제든 환영합니다.
        </p>
        <div class="contact-links fade-in-up">
          <a class="contact-link" :href="emailLink.href">
            <span class="link-icon">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                <rect x="2" y="4" width="20" height="16" rx="2"/>
                <path d="m2 7 10 7 10-7"/>
              </svg>
            </span>
            <div class="link-body">
              <span class="link-label">Email</span>
              <span class="link-value">{{ emailLink.value }}</span>
            </div>
            <span class="link-arrow">→</span>
          </a>
          <a class="contact-link" :href="instagramLink.href" target="_blank" rel="noopener noreferrer">
            <span class="link-icon">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                <rect x="2" y="2" width="20" height="20" rx="5"/>
                <circle cx="12" cy="12" r="5"/>
                <circle cx="17.5" cy="6.5" r="1" fill="currentColor" stroke="none"/>
              </svg>
            </span>
            <div class="link-body">
              <span class="link-label">Instagram</span>
              <span class="link-value">{{ instagramLink.value }}</span>
            </div>
            <span class="link-arrow">→</span>
          </a>
        </div>
      </div>

      <div class="contact-form fade-in-up">
        <div class="form-group">
          <label class="form-label">이름</label>
          <input class="form-input" type="text" placeholder="홍길동" v-model="form.name">
        </div>
        <div class="form-group">
          <label class="form-label">이메일</label>
          <input class="form-input" type="email" placeholder="your@email.com" v-model="form.email">
        </div>
        <div class="form-group">
          <label class="form-label">메시지</label>
          <textarea class="form-textarea" placeholder="안녕하세요, ..." v-model="form.message"></textarea>
        </div>
        <button class="form-submit" @click="handleSubmit">Send Message</button>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'
const props = defineProps({ contactLinks: Array })
const emailLink = computed(() => props.contactLinks.find((l) => l.label === 'Email'))
const instagramLink = computed(() => props.contactLinks.find((l) => l.label === 'Instagram'))
const form = ref({ name: '', email: '', message: '' })
const handleSubmit = () => { alert('메시지가 전송되었습니다!') }
</script>

<style scoped>
#contact { background: var(--dark-ink); color: var(--cream); }
#contact .section-num { color: #1a1510; }
#contact .section-title { color: var(--cream); }

.contact-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 80px; align-items: start; }

.contact-tagline {
  font-family: 'Cormorant Garamond', serif; font-size: 34px; font-weight: 300;
  font-style: italic; line-height: 1.3; color: var(--cream); margin-bottom: 40px;
}
.contact-tagline em { color: var(--gold); font-style: normal; }

.contact-links { display: flex; flex-direction: column; }
.contact-link {
  display: flex; align-items: center; gap: 20px; padding: 22px 0;
  border-bottom: 1px solid rgba(255,255,255,0.08);
  text-decoration: none; color: var(--cream); transition: padding-left 0.3s ease;
}
.contact-link:hover { padding-left: 8px; }
.link-icon {
  display: flex; align-items: center; justify-content: center;
  width: 36px; height: 36px;
  border: 1px solid rgba(255,255,255,0.15); border-radius: 50%;
  color: rgba(255,255,255,0.5); transition: color 0.3s, border-color 0.3s; flex-shrink: 0;
}
.contact-link:hover .link-icon { color: var(--gold); border-color: var(--gold); }
.link-body { display: flex; flex-direction: column; flex: 1; }
.link-label { font-size: 9px; letter-spacing: 0.25em; text-transform: uppercase; color: var(--warm-gray); margin-bottom: 3px; }
.link-value { font-family: 'Cormorant Garamond', serif; font-size: 20px; font-weight: 300; }
.link-arrow { font-size: 18px; color: rgba(255,255,255,0.2); transition: color 0.3s; }
.contact-link:hover .link-arrow { color: var(--gold); }

.contact-form { display: flex; flex-direction: column; gap: 24px; }
.form-group { display: flex; flex-direction: column; gap: 8px; }
.form-label { font-size: 9px; letter-spacing: 0.25em; text-transform: uppercase; color: var(--warm-gray); }
.form-input, .form-textarea {
  background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.1);
  color: var(--cream); padding: 14px 18px;
  font-family: 'Montserrat', sans-serif; font-size: 13px;
  outline: none; transition: border-color 0.3s; resize: none;
}
.form-input:focus, .form-textarea:focus { border-color: var(--gold); }
.form-textarea { height: 120px; }
.form-submit {
  background: var(--gold); color: var(--dark-ink); border: none; padding: 16px 40px;
  font-family: 'Montserrat', sans-serif; font-size: 10px; letter-spacing: 0.25em;
  text-transform: uppercase; cursor: pointer; transition: background 0.3s;
  align-self: flex-start; font-weight: 500;
}
.form-submit:hover { background: var(--gold-light); }

/* 태블릿 */
@media (max-width: 1024px) {
  .contact-grid { gap: 48px; }
  .contact-tagline { font-size: 28px; }
}

/* 모바일 */
@media (max-width: 768px) {
  #contact { padding: 80px 24px; }
  .contact-grid { grid-template-columns: 1fr; gap: 48px; }
  .contact-tagline { font-size: 26px; }
  .link-value { font-size: 16px; }
  .form-submit { width: 100%; text-align: center; }
}
</style>
