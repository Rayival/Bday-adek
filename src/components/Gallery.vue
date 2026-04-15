<template>
  <div class="wrapper">

    <!-- 🌌 background -->
    <div class="bg"></div>

    <!-- 🌫️ glow -->
    <div class="glow g1"></div>
    <div class="glow g2"></div>

    <!-- ✨ floating (safe) -->
    <div class="floating">
      <span v-for="i in 6" :key="i" :style="randomStyle()">💙</span>
      <span v-for="i in 4" :key="'s'+i" :style="randomStyle()">✨</span>
    </div>

    <!-- 💎 content -->
    <div class="content">

      <h1 class="title">little moments ✨</h1>

      <p class="subtitle">
        some small memories that still feel special
      </p>

      <!-- 📸 GRID -->
      <div class="grid">

        <div
          v-for="(item, i) in items"
          :key="i"
          class="card group"
          :style="{ animationDelay: i * 0.12 + 's' }"
        >

          <!-- glow overlay -->
          <div class="overlay"></div>

          <!-- shine effect -->
          <div class="shine"></div>

          <!-- media -->
          <div class="media-wrap">

          <!-- IMAGE -->
          <img 
            v-if="item.type === 'img'" 
            :src="item.src" 
            class="media-img"
          />

          <!-- VIDEO -->
          <video 
            v-else 
            controls 
            class="media-video"
          >
            <source :src="item.src" />
          </video>

        </div>

          <!-- text -->
          <div class="text">
            <h2 class="card-title">{{ item.title }}</h2>
            <p class="card-desc">{{ item.desc }}</p>
          </div>

        </div>

      </div>

      <!-- 💙 FINAL CARD -->
      <div class="card final-card">

        <div class="overlay"></div>
        <div class="shine"></div>

        <div class="final-content">

          <div class="final-icon">⭐⭐⭐⭐⭐</div>

          <p class="final-text">
            makasihh banyakk yaa ade,<br/>
            moment sekecil apapun kalo sama kamu<br/>
            ituu berartii bangett buatt akuuu
          </p>

        </div>

      </div>

      <!-- button -->
      <button @click="$emit('next')" class="btn">
        continue →
      </button>

    </div>

  </div>
</template>

<script setup>
import foto1 from '@/assets/img/foto1.jpg'
import foto2 from '@/assets/img/foto2.jpg'
import foto3 from '@/assets/img/foto3.jpg'
import video1 from '../assets/video/video1.mp4'

const items = [
  {
    type: 'img',
    src: foto1,
    title: 'a quiet night in the rain',
    desc: 'malam itu kita ujanan… inget banget suasananya dinginn. aa nemenin kamu di jalan karena jujur aa khawatir… takut kamu kenapa-napa. tapi anehnya, di tengah rasa khawatir itu aa malah ngerasa seneng bangettt sesimpel itu aja udah bikin aa ngerasa hangat. kayak… aa pengen momen itu ga cepet selesai. sampai sekarang kalau inget itu, rasanya masih sama… hangat dan tenang.'
  },
  {
    type: 'img',
    src: foto2,
    title: 'our first little moment',
    desc: 'ini pertama kalinya kita tos… keliatannya kaya hal kecil banget yaa, bahkan mungkin biasa aja buat orang lain. tapi buat aa, itu beda. dari hal kecil itu justru buat aa ngerasa nyaman… ngerasa ada sesuatu yang spesial tanpa harus dijelasin. lucunya, justru moment kecil kayak gini yang paling sering keinget sampai sekarang '
  },
  {
    type: 'img',
    src: foto3,
    title: 'when we started talking',
    desc: 'ini pertama kali kita ngobrol, duduk deketann dan masih malu-malu banget, bahkan pas fotbar juga keliatan kaku 😭 tapi justru itu yang bikin semuanya kerasa jujur. ga ada yang dibuat-buat, semuanya ngalir aja. dari situ aa mulai kenal kamu pelan-pelan… cara kamu ngomong, cara kamu bersikap… dan tanpa sadar, dari moment sesimpel itu aa mulai ngerasa kamu berarti.'
  },
  {
    type: 'video',
    src: video1,
    title: 'a simple night together',
    desc: 'di video ini keliatannya sederhana banget… kita tos lagi, aa nemenin kamu jalan karena udah malem. tapi justru itu yang bikin berarti. bukan karena tempatnya, bukan karena momentnya harus besar… tapi karena itu sama kamu. jujur, moment kecil kayak gini yang paling sering aa inget. karena di situ aa ngerasa bener-bener seneng… dengan cara yang sederhana, tapi tulus banget.'
  }
]

const randomStyle = () => ({
  left: Math.random() * 100 + "%",
  animationDuration: 6 + Math.random() * 6 + "s"
})
</script>

<style scoped>

/* wrapper */
.wrapper {
  @apply relative overflow-hidden px-4;
  min-height: 100dvh;
  padding-top: clamp(80px, 10vh, 140px);
  padding-bottom: clamp(80px, 10vh, 140px);
}

/* FOTO (tetap landscape) */
.media-img {
  @apply w-full h-[180px] md:h-[260px] object-cover;
  transition: 0.6s;
}

/* VIDEO (story mode 9:16 🔥) */
.media-video {
  width: 100%;
  aspect-ratio: 9 / 16;
  object-fit: cover;
  border-radius: 12px;
  transition: 0.6s;
  box-shadow: 
    0 10px 30px rgba(0,0,0,0.4),
    0 0 0 1px rgba(255,255,255,0.1);
}

/* bg */
.bg {
  position: absolute;
  inset: 0;
  background: linear-gradient(120deg, #020617, #0f172a, #020617);
}

/* glow */
.glow {
  position: absolute;
  border-radius: 9999px;
  filter: blur(140px);
  opacity: 0.25;
  pointer-events: none;
}

.g1 {
  width: 350px;
  height: 350px;
  background: #3b82f6;
  top: -120px;
  left: -120px;
}

.g2 {
  width: 250px;
  height: 250px;
  background: #60a5fa;
  bottom: -120px;
  right: -120px;
}

/* floating */
.floating span {
  position: absolute;
  font-size: 14px;
  opacity: 0.15;
  animation: floatUp linear infinite;
  pointer-events: none;
}

/* 💙 FINAL CARD */
.final-card {
  @apply flex items-center justify-center text-center;
  min-height: 180px;
  grid-column: span 2;
  margin-top: 28px;
  background: linear-gradient(
    135deg,
    rgba(255,255,255,0.06),
    rgba(59,130,246,0.08)
  );
}

/* content tengah */
.final-content {
  padding: 28px 24px;
}

/* icon */
.final-icon {
  font-size: 28px;
  margin-bottom: 10px;

  animation: pulse 2s infinite;
}

/* text */
.final-text {
  font-family: 'Caveat', cursive;
  font-size: 18px;

  color: #93c5fd;
  line-height: 1.6;

  text-shadow: 0 0 12px rgba(96,165,250,0.4);
}

/* anim */
@keyframes pulse {
  0%,100% { transform: scale(1); }
  50% { transform: scale(1.15); }
}

/* content */
.content {
  @apply text-center z-10 max-w-5xl w-full mx-auto relative;
}

/* title */
.title {
  font-family: 'Playfair Display', serif;
  @apply text-3xl md:text-5xl text-white;
}

/* subtitle */
.subtitle {
  @apply text-sm md:text-base text-blue-300 mt-3;
}

/* grid */
.grid {
  display: grid;
  gap: 16px;
  margin-top: 40px;
}

@media (min-width: 768px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 24px;
  }
}

/* card */
.card {
  @apply relative bg-white/5 backdrop-blur-xl border border-white/10 rounded-2xl overflow-hidden;
  animation: fadeUp 0.6s ease forwards;
  opacity: 0;
  transform: translateY(30px);
  transition: 0.4s;
}

/* overlay glow */
.overlay {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle, rgba(59,130,246,0.3), transparent);
  opacity: 0;
  transition: 0.4s;
  pointer-events: none;
}

/* shine */
.shine {
  position: absolute;
  inset: 0;
  background: linear-gradient(120deg, transparent, rgba(255,255,255,0.15), transparent);
  opacity: 0;
  transition: 0.6s;
}

/* hover */
.card:hover {
  transform: translateY(-12px) scale(1.04);
  box-shadow: 0 30px 100px rgba(0,0,0,0.6);
}

.card:hover .overlay {
  opacity: 1;
}

.card:hover .shine {
  opacity: 1;
  transform: translateX(100%);
}

/* media */
.media-wrap {
  overflow: hidden;
}

.media {
  @apply w-full h-[180px] md:h-[260px] object-cover;
  transition: 0.6s;
}

.card:hover .media {
  transform: scale(1.1);
}

/* text */
.text {
  @apply p-4 text-left;
}

.card-title {
  @apply text-white font-semibold text-lg;
}

.card-desc {
  @apply text-blue-300 text-sm mt-1;
}

/* button */
.btn {
  @apply mt-12 px-6 py-3 rounded-full bg-white/10 backdrop-blur border border-white/20 text-white transition;
}

.btn:hover {
  transform: scale(1.05);
}

/* animations */
@keyframes fadeUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes floatUp {
  from { transform: translateY(0); }
  to { transform: translateY(-120vh); opacity: 0; }
}

</style>