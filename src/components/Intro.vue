<template>
  <div class="wrapper">

    <!-- 🌌 background -->
    <div class="bg"></div>

    <!-- 🌫️ glow -->
    <div class="glow g1"></div>
    <div class="glow g2"></div>

    <!-- ✨ floating -->
    <div class="floating">
      <span v-for="i in 6" :key="i" :style="randomStyle()">💙</span>
      <span v-for="i in 3" :key="'s'+i" :style="randomStyle()">✨</span>
    </div>

    <!-- 🎁 visual ringan -->
    <div class="visual">
      <div class="box">
        💙
      </div>

      <div class="sparkle">
        ✨
      </div>
    </div>

    <!-- 💎 content -->
    <div class="content">

      <h1 class="heading">
        {{ displayedTextLine1 }}
      </h1>

      <h2 class="highlight">
        {{ displayedTextLine2 }}
      </h2>

      <p class="sub">
        a small story made with care
      </p>

      <button v-if="done" @click="$emit('next')" class="btn">
        klik pelan-pelan yaa 💙 →
      </button>

    </div>

  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const line1 = "hai adee..."
const line2 = "aa ada sesuatu kecil nih 😄"

const displayedTextLine1 = ref("")
const displayedTextLine2 = ref("")
const done = ref(false)

onMounted(async () => {
  await typeLine(line1, displayedTextLine1)
  await delay(400)
  await typeLine(line2, displayedTextLine2)

  setTimeout(() => {
    done.value = true
  }, 500)
})

const typeLine = (text, target) => {
  return new Promise((resolve) => {
    let i = 0
    const typing = () => {
      if (i < text.length) {
        target.value += text[i]
        i++
        setTimeout(typing, 30 + Math.random() * 40)
      } else {
        resolve()
      }
    }
    typing()
  })
}

const delay = (ms) => new Promise(res => setTimeout(res, ms))

const randomStyle = () => ({
  left: Math.random() * 100 + "%",
  animationDuration: 6 + Math.random() * 6 + "s"
})
</script>

<style scoped>

/* 🌌 wrapper */
.wrapper {
  @apply min-h-screen flex items-center justify-center relative overflow-hidden;
}

/* 🌌 background */
.bg {
  position: absolute;
  inset: 0;
  background: linear-gradient(120deg, #020617, #0f172a, #020617);
}

/* 🌫️ glow */
.glow {
  position: absolute;
  border-radius: 9999px;
  filter: blur(150px);
  opacity: 0.25;
  animation: moveGlow 12s ease-in-out infinite alternate;
}

.g1 {
  width: 500px;
  height: 500px;
  background: #3b82f6;
  top: -120px;
  left: -120px;
}

.g2 {
  width: 300px;
  height: 300px;
  background: #60a5fa;
  bottom: -120px;
  right: -120px;
}

/* ✨ floating */
.floating span {
  position: absolute;
  bottom: -10px;
  font-size: 12px;
  opacity: 0.15;
  animation: floatUp linear infinite;
}

/* 🎁 visual */
.visual {
  position: absolute;
  top: 18%;
  left: 50%;
  transform: translateX(-50%);
  z-index: 5;
}

/* box kecil (ringan) */
.box {
  width: 80px;
  height: 80px;
  background: rgba(255,255,255,0.05);
  backdrop-filter: blur(15px);
  border-radius: 18px;

  display: flex;
  align-items: center;
  justify-content: center;

  font-size: 28px;
  color: white;

  box-shadow: 0 20px 40px rgba(0,0,0,0.3);
}

/* sparkle kecil */
.sparkle {
  position: absolute;
  right: -15px;
  bottom: -15px;

  width: 40px;
  height: 40px;

  background: white;
  border-radius: 999px;

  display: flex;
  align-items: center;
  justify-content: center;

  font-size: 16px;

  box-shadow: 0 10px 30px rgba(0,0,0,0.3);
}

/* 💎 content */
.content {
  @apply text-center px-6 z-10 max-w-xl;
}

/* typography */
.heading {
  font-family: 'Playfair Display', serif;
  @apply text-3xl md:text-6xl text-white font-semibold;
}

.highlight {
  font-family: 'Playfair Display', serif;
  @apply text-3xl md:text-6xl italic text-blue-400 mt-2;
}

.sub {
  font-family: 'Inter', sans-serif;
  @apply text-xs tracking-[0.3em] text-blue-300 mt-6 uppercase;
}

/* button */
.btn {
  @apply mt-10 px-6 md:px-8 py-3 rounded-full bg-white/10 backdrop-blur border border-white/20 text-white transition;
}

.btn:hover {
  transform: scale(1.05);
  background: rgba(255,255,255,0.2);
}

/* animasi */
@keyframes moveGlow {
  from { transform: translateY(0); }
  to { transform: translateY(20px); }
}

@keyframes floatUp {
  from { transform: translateY(0); }
  to { transform: translateY(-120vh); opacity: 0; }
}

</style>