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
      <span v-for="i in 2" :key="'s'+i" :style="randomStyle()">✨</span>
    </div>

    <!-- 🎁 VISUAL ICON -->
    <div class="visual">
      <div class="box">
        <Gift class="gift-icon" />
      </div>

      <div class="sparkle">
        <Sparkles class="sparkle-icon" />
      </div>
    </div>

    <!-- 💎 content -->
    <div class="content">

      <h1 class="title">
        i have something small...
      </h1>

      <h2 class="highlight">
        just for you ✨
      </h2>

      <p class="sub">
        a simple little story, but meaningful
      </p>

      <button @click="$emit('next')" class="btn">
        <Gift class="w-5 h-5" />
        start slowly 💙
      </button>

      <!-- <p class="hint">
        (take it easy, no rush)
      </p> -->

    </div>

  </div>
</template>

<script setup>
import { Gift, Sparkles } from 'lucide-vue-next'

const randomStyle = () => ({
  left: Math.random() * 100 + "%",
  animationDuration: 6 + Math.random() * 6 + "s"
})
</script>

<style scoped>

/* 🌌 wrapper */
.wrapper {
  @apply min-h-screen flex items-center justify-center relative overflow-hidden px-4;
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
  filter: blur(140px);
  opacity: 0.25;
  animation: moveGlow 12s ease-in-out infinite alternate;
}

.g1 {
  width: 400px;
  height: 400px;
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
  top: 12%;
  left: 50%;
  transform: translateX(-50%);
  z-index: 5;
}

/* box responsive */
.box {
  width: 90px;
  height: 90px;
  background: rgba(255,255,255,0.05);
  backdrop-filter: blur(20px);
  border-radius: 20px;

  display: flex;
  align-items: center;
  justify-content: center;

  box-shadow: 0 20px 60px rgba(0,0,0,0.4);

  transform: rotate(-10deg);
}

@media (min-width: 768px) {
  .box {
    width: 130px;
    height: 130px;
  }
}

/* icon utama */
.gift-icon {
  width: 28px;
  height: 28px;
  color: white;
}

@media (min-width: 768px) {
  .gift-icon {
    width: 40px;
    height: 40px;
  }
}

/* sparkle */
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

  box-shadow: 0 10px 30px rgba(0,0,0,0.3);
}

.sparkle-icon {
  width: 18px;
  height: 18px;
  color: #3b82f6;
}

/* 💎 content */
.content {
  @apply text-center z-10 max-w-md md:max-w-xl mt-32 md:mt-40;
}

/* typography */
.title {
  font-family: 'Playfair Display', serif;
  @apply text-2xl md:text-5xl text-white font-semibold;
}

.highlight {
  font-family: 'Playfair Display', serif;
  @apply text-2xl md:text-5xl italic text-blue-400 mt-2;
}

.sub {
  font-family: 'Inter', sans-serif;
  @apply text-[10px] md:text-xs tracking-[0.25em] text-blue-300 mt-5 uppercase;
}

/* button */
.btn {
  @apply mt-8 md:mt-10 px-6 md:px-8 py-3 rounded-full bg-white/10 backdrop-blur border border-white/20 text-white flex items-center gap-2 mx-auto transition;
}

.btn:hover {
  transform: scale(1.05);
  background: rgba(255,255,255,0.2);
  box-shadow: 0 0 20px rgba(59,130,246,0.3);
}

.btn:active {
  transform: scale(0.95);
}

/* hint */
.hint {
  @apply text-xs text-blue-400 mt-3 opacity-70;
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