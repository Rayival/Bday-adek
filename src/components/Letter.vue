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

      <!-- 📖 letter -->
      <div class="letter">

        <p class="text">
          <span v-html="displayed"></span>
          <span class="cursor">|</span>
        </p>

      </div>

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
  "happy birthday yaa... 🎂",
  "",
  "aku bingung mulai dari mana...",
  "tapi mungkin aku mulai dari ini dulu...",
  "",
  "<b>makasih ya...</b>",
  "udah hadir di dunia ini.",
  "",
  "dan makasih juga...",
  "pernah ada di hidup aku, walaupun ga selamanya.",
  "",
  "jujur...",
  "di hari kayak gini aku jadi banyak keinget hal-hal lama.",
  "",
  "hal-hal kecil yang mungkin dulu keliatan biasa aja...",
  "tapi sekarang kerasa banget artinya buat aku.",
  "",
  "cara kita ngobrol...",
  "candaan random kita...",
  "dan semua momen sederhana itu...",
  "ternyata ninggalin sesuatu yang ga sederhana.",
  "",
  "aku sadar...",
  "dulu aku belum bisa jadi yang terbaik buat kamu.",
  "",
  "bahkan mungkin...",
  "aku masih sering bikin kamu kecewa tanpa aku sadar.",
  "",
  "<b>dan aku minta maaf ya...</b>",
  "kalau dulu banyak kurangnya aku...",
  "kalau ada sikap aku yang nyakitin atau bikin kamu ga nyaman.",
  "",
  "sekarang aku lagi belajar...",
  "pelan-pelan memperbaiki diri aku.",
  "",
  "dan kamu harus tau...",
  "<b>kamu itu salah satu alasan terbesar aku berubah.</b>",
  "",
  "karena kamu...",
  "aku belajar buat lebih menghargai orang lain.",
  "aku belajar buat jadi lebih dewasa.",
  "dan aku belajar buat jadi versi diri aku yang lebih baik.",
  "",
  "makasih ya...",
  "karena selama ini kamu selalu baik sama aku.",
  "",
  "kamu selalu hargain aku...",
  "selalu support aku...",
  "bahkan di saat aku belum jadi siapa-siapa.",
  "",
  "dan jujur aja...",
  "<b>itu berarti banget buat aku.</b>",
  "",
  "aku mungkin ga selalu nunjukin...",
  "tapi aku selalu inget semuanya.",
  "",
  "dan sampai sekarang...",
  "",
  "<b>aku masih sayang banget sama kamu.</b>",
  "",
  "perasaan itu ga pernah bener-bener hilang...",
  "cuma aku simpen, aku jaga, dan aku perbaiki pelan-pelan.",
  "",
  "aku ga tau ke depannya gimana...",
  "aku juga ga mau maksa apapun.",
  "",
  "tapi kalau ada satu hal yang pasti...",
  "",
  "<span class='hand'>aku selalu pengen liat kamu bahagia.</span>",
  "",
  "dengan atau tanpa aku.",
  "",
  "semoga di umur kamu yang sekarang...",
  "semua hal baik dateng ke kamu.",
  "",
  "semoga kamu selalu dikelilingi orang-orang yang sayang sama kamu...",
  "dan semoga semua yang kamu harapin bisa tercapai.",
  "",
  "dan kalau suatu hari nanti...",
  "kita dipertemukan lagi dengan versi kita yang lebih baik...",
  "",
  "aku harap kita bisa ngobrol lagi...",
  "tanpa rasa asing.",
  "",
  "once again...",
  "",
  "<b>happy birthday 💙</b>"
];

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

/* heading */
.heading {
  font-family: 'Playfair Display', serif;
  @apply text-3xl md:text-5xl text-white mb-6;
}

/* letter */
.letter {
  @apply bg-white/5 backdrop-blur-xl border border-white/10 rounded-2xl p-6 md:p-10 text-left;
}

/* text */
.text {
  font-family: 'Inter', sans-serif;
  @apply text-sm md:text-base text-blue-100 leading-relaxed;
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

</style>