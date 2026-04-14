<template>
  <div class="wrapper">

    <!-- 🌌 background -->
    <div class="bg"></div>

    <!-- 🌫️ glow -->
    <div class="glow g1"></div>
    <div class="glow g2"></div>

    <!-- ✨ floating -->
    <div class="floating">
      <span v-for="i in 5" :key="i" :style="randomStyle()">💙</span>
      <span v-for="i in 3" :key="'s'+i" :style="randomStyle()">✨</span>
    </div>

    <!-- 💎 content -->
    <div class="content">

      <!-- 📝 title -->
      <h1 class="heading">for you ✨</h1>

      <svg class="svg-top" viewBox="0 0 400 100">
        <path d="M0 50 Q100 10 200 50 T400 50" />
      </svg>

      <!-- 📖 letter -->
      <div class="letter">

        <div class="icon-overlay">💙</div>

        <p class="text">
          <span v-html="displayed"></span>
          <span class="cursor">|</span>
        </p>

      </div>

      <svg class="svg-bottom" viewBox="0 0 400 100">
        <path d="M0 50 Q100 90 200 50 T400 50" />
      </svg>

      <!-- button -->
      <button v-if="done" @click="$emit('next')" class="btn">
        last one 💙 →
      </button>

    </div>

  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const displayed = ref("")
const done = ref(false)

/* 💙 isi lebih panjang + campur indo english + minta maaf */
const sentences = [
  "selamat ulang tahun yaa 🎂",
  "",
  "hari ini mungkin cuma satu hari biasa buat banyak orang…",
  "tapi buat aku… hari ini spesial banget.",
  "",
  "hari dimana seseorang yang berarti banget di hidup aku lahir ke dunia ini.",
  "",
  "aku harap di umur kamu yang sekarang…",
  "semua hal baik selalu deket sama kamu.",
  "",
  "semoga kamu selalu dikelilingi orang-orang yang tulus…",
  "selalu diberi kebahagiaan…",
  "dan semua yang kamu usahakan pelan-pelan bisa tercapai.",
  "",
  "aamiinn",
  "",
  "aku juga mau jujur sedikit…",
  "",
  "kalau dipikir-pikir ke belakang…",
  "aku ngerasa dulu aku belum jadi versi terbaik dari diri aku.",
  "",
  "bahkan hal kecil kayak ngasih sesuatu ke kamu aja…",
  "aku belum pernah.",
  "",
  "dan entah kenapa…",
  "itu selalu kepikiran sampai sekarang.",
  "",
  "makanya di momen ini…",
  "aku pengen memperbaiki itu.",
  "",
  "walaupun sederhana…",
  "tapi ini bener-bener tulus dari aku.",
  "",
  "aku masih inget gimana kamu dari dulu sampai sekarang…",
  "",
  "cara kamu bersikap…",
  "cara kamu memperlakukan aku dengan baik…",
  "cara kamu selalu menghargai aku…",
  "",
  "bahkan di saat aku sendiri…",
  "belum tentu bisa menghargai diri aku sendiri.",
  "",
  "kamu itu…",
  "<b>selalu baik.</b>",
  "<b>selalu support aku.</b>",
  "<b>selalu ada.</b>",
  "",
  "dan tanpa kamu sadar…",
  "",
  "<b>kamu jadi salah satu alasan terbesar aku buat berkembang.</b>",
  "",
  "aku berubah pelan-pelan…",
  "aku belajar banyak hal…",
  "",
  "dan jujur…",
  "di balik semua itu, ada kamu.",
  "",
  "kamu yang jadi alasan diam-diam aku buat jadi lebih baik.",
  "",
  "",
  "<b>maafin aku ya adee…</b>",
  "",
  "selama ini aku banyak salah.",
  "banyak bikin kamu kecewa…",
  "banyak bikin kamu sedih…",
  "",
  "bahkan mungkin…",
  "pernah bikin kamu nangis.",
  "",
  "dan jujur…",
  "kalau aku inget itu semua…",
  "",
  "<b>aku juga ikut sakit.</b>",
  "",
  "tapi sekarang aku lagi belajar…",
  "belajar jadi pribadi yang lebih baik.",
  "pelan-pelan…",
  "",
  "aku ga janji jadi sempurna…",
  "tapi aku janji bakal terus berusaha.",
  "",
  "setidaknya jadi versi yang lebih baik dari yang dulu.",
  "",
  "",
  "aku juga mau bilang sesuatu…",
  "",
  "yang mungkin sederhana…",
  "tapi ini jujur dari hati aku",
  "",
  "<b>aku selalu sayang banget sama kamu.</b>",
  "",
  "aku ga mau bikin semuanya jadi berat…",
  "",
  "aku cuma pengen kamu ngerasa satu hal:",
  "",
  "bahwa kamu dihargai…",
  "bahwa kehadiran kamu berarti…",
  "",
  "dan bahwa ada seseorang di sini…",
  "yang selalu doain kamu dengan tulus…",
  "",
  "selalu bangga sama kamu…",
  "dan selalu dukung kamu.",
  "",
  "",
  "sekali lagi…",
  "",
  "<b>selamat ulang tahun yaa </b>",
  "",
  "semoga hari kamu hangat…",
  "penuh senyum…",
  "dan penuh hal-hal baik.",
  "",
  "",
  "<span class='hand'>i'll always care about you… ilysm❤️.</span>"
]

const typeSentence = (sentence) => {
  return new Promise((resolve) => {
    let i = 0
    const typing = () => {
      if (i < sentence.length) {
        displayed.value += sentence[i]
        i++
        setTimeout(typing, 25 + Math.random() * 40)
      } else {
        displayed.value += "<br/>"
        resolve()
      }
    }
    typing()
  })
}

const delay = (ms) => new Promise(res => setTimeout(res, ms))

onMounted(async () => {
  for (let s of sentences) {
    await typeSentence(s)
    await delay(400 + Math.random() * 300)
  }
  await delay(1000)
  done.value = true
})

const randomStyle = () => ({
  left: Math.random() * 100 + "%",
  animationDuration: 6 + Math.random() * 6 + "s"
})
</script>

<style scoped>

/* wrapper */
.wrapper {
  @apply min-h-screen flex flex-col justify-start relative overflow-hidden px-4;
  padding-top: clamp(80px, 10vh, 140px);
  padding-bottom: clamp(80px, 10vh, 140px);
}

/* bg */
.bg {
  position: absolute;
  inset: 0;
  background: linear-gradient(120deg, #020617, #0f172a, #020617);
}

.svg-top, .svg-bottom {
  width: 100%;
}

.svg-top path {
  stroke: #60a5fa;
  stroke-width: 1.5;
  fill: none;
  opacity: 0.2;
}

.svg-bottom path {
  stroke: #60a5fa;
  stroke-width: 1.5;
  fill: none;
  opacity: 0.15;
}

.icon-overlay {
  position: absolute;
  top: -20px;
  right: -20px;
  font-size: 60px;
  opacity: 0.05;
  pointer-events: none;
  filter: blur(2px);
}

/* glow */
.glow {
  position: absolute;
  border-radius: 9999px;
  filter: blur(140px);
  opacity: 0.25;
}

/* floating */
.floating span {
  position: absolute;
  bottom: -10px;
  font-size: 14px;
  opacity: 0.15;
  animation: floatUp linear infinite;
}

/* content */
.content {
  @apply text-center z-10 max-w-2xl mx-auto;
}
.content::before {
  content: "";
  position: absolute;
  width: 400px;
  height: 400px;
  background: radial-gradient(circle, rgba(59,130,246,0.15), transparent);
  filter: blur(100px);
  left: 50%;
  top: 40%;
  transform: translate(-50%, -50%);
  z-index: -1;
}

/* heading */
.heading {
  font-family: 'Playfair Display', serif;
  @apply text-3xl md:text-5xl text-white mb-6;
}

/* letter */
.letter {
  @apply bg-white/5 backdrop-blur-xl border border-white/10 rounded-2xl p-6 md:p-10 text-left;
  box-shadow: 
    0 20px 60px rgba(0,0,0,0.4),
    inset 0 1px 0 rgba(255,255,255,0.1);
    animation: fadeUp 1s ease;
}

/* text */
.text {
  font-family: 'Inter', sans-serif;
  @apply text-sm md:text-base text-blue-100 leading-relaxed tracking-wide;
}

/* highlight */
.text b {
  @apply text-blue-400 font-semibold;
}

/* handwriting */
.hand {
  font-family: 'Caveat', cursive;
  @apply text-blue-300 text-lg;
}

/* cursor */
.cursor {
  animation: blink 1s infinite;
}

/* button */
.btn {
  @apply mt-10 px-6 py-3 rounded-full bg-white/10 backdrop-blur border border-white/20 text-white transition;
}

.btn:hover {
  transform: scale(1.05);
}

/* animasi */
@keyframes floatUp {
  from { transform: translateY(0); }
  to { transform: translateY(-120vh); opacity: 0; }
}

@keyframes blink {
  0%,100% { opacity: 1; }
  50% { opacity: 0; }
}

@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

</style>