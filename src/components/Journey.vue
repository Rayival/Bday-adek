<template>
  <div class="wrapper">

    <!-- 🌌 background -->
    <div class="bg"></div>

    <!-- 🌫️ glow (safe layer) -->
    <div class="glow g1"></div>
    <div class="glow g2"></div>

    <!-- 💎 layout -->
    <div class="container">

      <!-- ✨ TEXT -->
      <div class="text-block">
        <h1 class="title">it started simply...</h1>

        <h2 class="highlight">just something small</h2>

        <p class="sub">
          but somehow, it stayed longer than expected
        </p>

        <button @click="$emit('next')" class="btn">
          continue →
        </button>
      </div>

      <!-- 🎁 VISUAL -->
      <div class="visual">

        <!-- animated rings -->
        <div class="ring r1"></div>
        <div class="ring r2"></div>
        <div class="ring r3"></div>

        <!-- glass card -->
        <div class="box">
          <Gift class="icon" />
        </div>

      </div>

    </div>

  </div>
</template>

<script setup>
import { Gift } from 'lucide-vue-next'
</script>

<style scoped>

/* 🌌 WRAPPER */
.wrapper {
  @apply min-h-screen flex items-center justify-center relative overflow-hidden px-5 md:px-8;
}

/* 🌌 BG */
.bg {
  position: absolute;
  inset: 0;
  background: linear-gradient(120deg, #020617, #0f172a, #020617);
}

/* 🌫️ GLOW (NO BLOCK CLICK) */
.glow {
  position: absolute;
  border-radius: 9999px;
  filter: blur(140px);
  opacity: 0.25;
  pointer-events: none;
  z-index: 0;
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

/* 💎 LAYOUT */
.container {
  @apply grid md:grid-cols-2 gap-10 md:gap-14 items-center max-w-5xl w-full;
  position: relative;
  z-index: 10;
}

/* ✨ TEXT */
.text-block {
  @apply text-center md:text-left;
}

.title {
  font-family: 'Playfair Display', serif;
  @apply text-2xl md:text-5xl text-white;
  animation: fadeUp 0.8s ease forwards;
}

.highlight {
  font-family: 'Playfair Display', serif;
  @apply text-2xl md:text-5xl italic text-blue-400 mt-2;
  animation: fadeUp 0.8s ease forwards;
  animation-delay: 0.3s;
}

.sub {
  @apply text-xs md:text-sm text-blue-300 mt-4 leading-relaxed;
  animation: fadeUp 0.8s ease forwards;
  animation-delay: 0.6s;
}

/* 🎁 VISUAL */
.visual {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* 💎 BOX */
.box {
  width: 110px;
  height: 110px;

  @media (min-width: 768px) {
    width: 140px;
    height: 140px;
  }

  background: rgba(255,255,255,0.05);
  backdrop-filter: blur(25px);
  border-radius: 28px;

  display: flex;
  align-items: center;
  justify-content: center;

  box-shadow: 0 25px 80px rgba(0,0,0,0.5);

  z-index: 3;

  animation: scaleIn 0.8s ease forwards;
}

/* 🎯 ICON */
.icon {
  width: 32px;
  height: 32px;

  @media (min-width: 768px) {
    width: 42px;
    height: 42px;
  }

  color: white;
}

/* 🔵 RINGS */
.ring {
  position: absolute;
  border-radius: 999px;
  border: 1px solid rgba(96,165,250,0.2);
  pointer-events: none;
}

.r1 {
  width: 150px;
  height: 150px;
  animation: pulse 3s infinite;
}

.r2 {
  width: 200px;
  height: 200px;
  animation: pulse 3s infinite;
  animation-delay: 1s;
}

.r3 {
  width: 260px;
  height: 260px;
  animation: pulse 3s infinite;
  animation-delay: 2s;
}

/* 🔘 BUTTON */
.btn {
  @apply mt-6 px-6 py-3 rounded-full bg-white/10 backdrop-blur border border-white/20 text-white transition;
  animation: fadeUp 0.8s ease forwards;
  animation-delay: 0.9s;

  position: relative;
  z-index: 20;
}

.btn:hover {
  transform: scale(1.05);
  background: rgba(255,255,255,0.2);
  box-shadow: 0 0 25px rgba(59,130,246,0.3);
}

/* 🎬 ANIMATIONS */
@keyframes pulse {
  0% {
    transform: scale(0.7);
    opacity: 0.4;
  }
  100% {
    transform: scale(1.5);
    opacity: 0;
  }
}

@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(15px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes scaleIn {
  from {
    opacity: 0;
    transform: scale(0.7);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

</style>