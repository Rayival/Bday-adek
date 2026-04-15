<template>
  <div class="wrapper">

    <!-- 🌌 background -->
    <div class="bg"></div>

    <!-- 🌫️ glow -->
    <div class="glow g1"></div>
    <div class="glow g2"></div>

    <!-- ✨ grain -->
    <div class="noise"></div>

    <!-- ✨ floating -->
    <div class="floating">
      <span v-for="i in 5" :key="i" :style="randomStyle()">💙</span>
      <span v-for="i in 3" :key="'s'+i" :style="randomStyle()">✨</span>
    </div>

    <!-- 💎 content -->
    <div class="content">

      <h1 class="heading">for you ✨</h1>

      <!-- SVG -->
      <svg class="svg-top" viewBox="0 0 400 100">
        <path d="M0 50 Q100 10 200 50 T400 50" />
      </svg>

      <!-- 📖 LETTER -->
      <div class="letter">

        <div class="icon-overlay">🫂💙</div>

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

const sentences = [
  "selamat ulang tahun yaa adekkk 🎂",
  "",
  "hari ini mungkin cuma satu hari biasa buat banyak orang…",
  "tapi buat aku… hari ini spesial bangettt.",
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
  "dan yaaa…",
  "itu selalu buat aku kepikiran sampai sekarang.",
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
  "<b>maafin aku ya adee…</b>",
  "",
  "selama ini aku banyak salah.",
  "banyak bikin kamu kecewa…",
  "banyak bikin kamu sedih…",
  "",
  "dan bahkan…",
  "bikin kamu nangis.",
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
  "aku juga mau bilang sesuatu…",
  "",
  "yang mungkin sederhana…",
  "tapi ini jujur dari hati aku",
  "",
  "<b>aku selalu sayangg bangett sama kamuu.</b>",
  "",
  "aku ga mau bikin semuanya jadi berat…",
  "",
  "aku cuma pengen kamu ngerasa satu hal",
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
  "<b>selamat ulang tahun yaa </b>",
  "",
  "semoga hari kamu hangat…",
  "penuh senyum…",
  "dan penuh hal-hal baik.",
  "",
  "<span class='hand'>i'll always care about you… ilysm💙.</span>",
  "<span class='signature'>— <a href='https://rayival.vercel.app' target='_blank'>Valdes</a></span>"
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

/* 🌌 WRAPPER */
.wrapper {
  @apply min-h-screen flex flex-col justify-start relative overflow-hidden px-4;
  padding-top: clamp(80px, 10vh, 140px);
  padding-bottom: clamp(80px, 10vh, 140px);
}

/* BG */
.bg {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at center, #0f172a, #020617);
}

/* vignette */
.wrapper::after {
  content: "";
  position: absolute;
  inset: 0;
  background: radial-gradient(circle, transparent 40%, rgba(0,0,0,0.8));
}

/* glow */
.glow {
  position: absolute;
  border-radius: 9999px;
  filter: blur(160px);
  opacity: 0.25;
  animation: float 12s infinite alternate;
}

/* grain */
.noise {
  position: absolute;
  inset: 0;
  background-image: url("https://grainy-gradients.vercel.app/noise.svg");
  opacity: 0.05;
}

.svg-top path,
.svg-bottom path {
  stroke: #60a5fa;
  stroke-width: 1.5;
  fill: none;
  opacity: 0.3;

  /* ✨ animasi biar hidup */
  stroke-dasharray: 500;
  stroke-dashoffset: 500;
  animation: drawLine 3s ease forwards;
}

@keyframes drawLine {
  to {
    stroke-dashoffset: 0;
  }
}

/* content */
.content {
  @apply text-center z-10 max-w-2xl mx-auto relative;
}

/* spotlight */
.content::before {
  content: "";
  position: absolute;
  width: 500px;
  height: 500px;
  background: radial-gradient(circle, rgba(59,130,246,0.2), transparent);
  filter: blur(120px);
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
  @apply relative bg-white/5 backdrop-blur-xl border border-white/10 rounded-2xl p-6 md:p-10 text-left;

  box-shadow:
    0 30px 80px rgba(0,0,0,0.6),
    inset 0 1px 0 rgba(255,255,255,0.1);

  overflow: hidden;
}

/* border glow */
.letter::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1px;
  background: linear-gradient(120deg, transparent, rgba(96,165,250,0.4), transparent);
  -webkit-mask: linear-gradient(#000 0 0) content-box, linear-gradient(#000 0 0);
  -webkit-mask-composite: xor;
}

/* text */
.text {
  font-family: 'DM Serif Display', serif;
  @apply text-[15px] md:text-[17px] text-blue-100 leading-[1.9];
  text-shadow:
    0 1px 0 rgba(255,255,255,0.05),
    0 10px 30px rgba(0,0,0,0.6);
  letter-spacing: 0.3px;
}

/* highlight */
.text b {
  color: #93c5fd;
  font-weight: 600;

  text-shadow: 0 0 10px rgba(96,165,250,0.3);
}

.signature {
  display: block;
  margin-top: 12px;

  font-family: 'Playfair Display', serif;
  font-size: 14px;

  color: #93c5fd;
  opacity: 0.8;

  letter-spacing: 1px;
}

/* link style */
.signature a {
  text-decoration: none;
  color: #60a5fa;

  font-weight: 500;

  border-bottom: 1px solid rgba(96,165,250,0.4);
  transition: all 0.3s ease;
}

/* hover effect */
.signature a:hover {
  color: white;
  border-bottom: 1px solid white;
}

/* handwriting */
.hand {
  font-family: 'Caveat', cursive;
  font-size: 20px;
  color: #93c5fd;

  text-shadow: 0 0 10px rgba(96,165,250,0.4);
}

/* button */
.btn {
  @apply mt-10 px-6 py-3 rounded-full bg-white/10 border border-white/20 text-white;
}

/* anim */
@keyframes float {
  from { transform: translateY(0); }
  to { transform: translateY(30px); }
}

</style>