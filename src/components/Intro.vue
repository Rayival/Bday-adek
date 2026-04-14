<template>
  <div class="wrapper">

    <!-- 🌌 background -->
    <div class="bg"></div>

    <!-- 🌫️ glow -->
    <div class="glow g1"></div>
    <div class="glow g2"></div>

    <!-- ✨ subtle particles -->
    <div class="particles">
      <span v-for="i in 6" :key="i" :style="randomStyle()"></span>
    </div>

    <!-- 💎 content -->
    <div class="content">

  <!-- ✨ TOP SVG -->
  <svg class="svg-top" viewBox="0 0 400 100">
    <path d="M0 50 Q100 10 200 50 T400 50" />
  </svg>

  <h1 class="heading">
    {{ line1 }}
  </h1>

  <h2 class="highlight">
    {{ line2 }}
  </h2>

  <p class="sub">
    a small story made with care
  </p>

  <!-- ✨ BOTTOM SVG -->
  <svg class="svg-bottom" viewBox="0 0 400 100">
    <path d="M0 50 Q100 90 200 50 T400 50" />
  </svg>

  <button v-if="showBtn" @click="$emit('next')" class="btn">
    continue →
  </button>

</div>

  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const line1 = ref("")
const line2 = ref("")
const showBtn = ref(false)

onMounted(() => {
  setTimeout(() => line1.value = "hey...", 300)
  setTimeout(() => line2.value = "i made something for you", 1000)
  setTimeout(() => showBtn.value = true, 1800)
})

const randomStyle = () => ({
  left: Math.random() * 100 + "%",
  animationDuration: 6 + Math.random() * 6 + "s"
})
</script>

<style scoped>

/* wrapper */
.wrapper {
  @apply min-h-screen flex items-center justify-center relative overflow-hidden px-4;
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

/* particles (super subtle) */
.particles span {
  position: absolute;
  width: 3px;
  height: 3px;
  background: white;
  opacity: 0.08;
  border-radius: 999px;
  animation: floatUp linear infinite;
}

/* content */
.content {
  @apply text-center z-10 max-w-2xl;
}

/* SVG TOP */
.svg-top {
  width: 100%;
  margin-bottom: 20px;
}

.svg-top path {
  stroke: #60a5fa;
  stroke-width: 1.5;
  fill: none;
  opacity: 0.25;

  stroke-dasharray: 400;
  stroke-dashoffset: 400;
  animation: drawLine 2s ease forwards;
}

/* SVG BOTTOM */
.svg-bottom {
  width: 100%;
  margin-top: 24px;
}

.svg-bottom path {
  stroke: #60a5fa;
  stroke-width: 1.5;
  fill: none;
  opacity: 0.15;
}

/* ✨ subtle glow tengah */
.content::before {
  content: "";
  position: absolute;
  width: 300px;
  height: 300px;
  background: radial-gradient(circle, rgba(59,130,246,0.15), transparent);
  filter: blur(80px);
  z-index: -1;
  left: 50%;
  top: 40%;
  transform: translate(-50%, -50%);
}

/* content fix */
.content {
  @apply text-center z-10 max-w-2xl relative;
}

/* heading */
.heading {
  font-family: 'Playfair Display', serif;
  @apply text-4xl md:text-6xl text-white font-semibold;
}

/* highlight */
.highlight {
  font-family: 'Playfair Display', serif;
  @apply text-4xl md:text-6xl italic text-blue-400 mt-2;
}

/* sub */
.sub {
  font-family: 'Inter', sans-serif;
  @apply text-xs tracking-[0.3em] text-blue-300 mt-6 uppercase;
}

/* button */
.btn {
  @apply mt-10 px-8 py-3 rounded-full bg-white/10 backdrop-blur border border-white/20 text-white transition;
  opacity: 0;
  animation: fadeUp 0.8s ease forwards;
  animation-delay: 1.8s;
}
.btn:hover {
  transform: scale(1.05);
  background: rgba(255,255,255,0.2);
}
.heading,
.highlight,
.sub {
  opacity: 0;
  transform: translateY(10px);
  animation: fadeUp 0.8s ease forwards;
}

.heading { animation-delay: 0.4s }
.highlight { animation-delay: 0.9s }
.sub { animation-delay: 1.4s }

@keyframes fadeUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* animasi */
@keyframes drawLine {
  to {
    stroke-dashoffset: 0;
  }
}
@keyframes floatUp {
  from { transform: translateY(0); }
  to { transform: translateY(-120vh); opacity: 0; }
}

</style>