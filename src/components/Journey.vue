<template>
  <div class="wrapper">

    <!-- 🌌 bg -->
    <div class="bg"></div>

    <!-- 🌫️ glow -->
    <div class="glow g1"></div>
    <div class="glow g2"></div>

    <!-- 🌌 vignette -->
    <div class="vignette"></div>

    <!-- ✨ particles -->
    <div class="particles">
      <span v-for="i in 8" :key="i" :style="randomParticle()"></span>
    </div>

    <!-- 💎 content -->
    <div class="content">

      <!-- 🎁 VISUAL -->
      <div class="visual">

        <!-- rings -->
        <div class="ring r1"></div>
        <div class="ring r2"></div>
        <div class="ring r3"></div>

        <!-- glow core -->
        <div class="orb"></div>

        <!-- glass box -->
        <div class="box">
          <Gift class="icon" />
        </div>

      </div>

      <!-- ✨ TEXT -->
      <div class="text-block">

        <h1 class="title fade1">
          it started simply...
        </h1>

        <h2 class="highlight fade2">
          just something small
        </h2>

        <p class="sub fade3">
          but somehow, it stayed longer than expected
        </p>

        <button @click="$emit('next')" class="btn fade4">
          continue →
        </button>

      </div>

    </div>

  </div>
</template>

<script setup>
import { Gift } from 'lucide-vue-next'

const randomParticle = () => ({
  left: Math.random() * 100 + "%",
  animationDuration: 6 + Math.random() * 6 + "s"
})
</script>

<style scoped>

/* 🌌 WRAPPER (SAFE MOBILE) */
.wrapper {
  @apply relative flex items-center justify-center overflow-hidden px-5;
  min-height: 100dvh;
  padding-top: clamp(80px, 12vh, 140px);
  padding-bottom: clamp(80px, 12vh, 140px);
}

/* BG */
.bg {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at center, #0f172a, #020617);
}

/* vignette cinematic */
.vignette {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle, transparent 40%, rgba(0,0,0,0.7));
}

/* glow */
.glow {
  position: absolute;
  border-radius: 9999px;
  filter: blur(160px);
  opacity: 0.25;
}

.g1 {
  width: 400px;
  height: 400px;
  background: #3b82f6;
  top: -150px;
  left: -150px;
}

.g2 {
  width: 300px;
  height: 300px;
  background: #60a5fa;
  bottom: -150px;
  right: -150px;
}

/* ✨ particles */
.particles span {
  position: absolute;
  bottom: -10px;
  width: 3px;
  height: 3px;
  background: white;
  opacity: 0.08;
  border-radius: 999px;
  animation: floatUp linear infinite;
}

/* CONTENT */
.content {
  @apply text-center z-10 max-w-xl w-full;
}

/* 🎁 VISUAL */
.visual {
  position: relative;
  margin-bottom: 40px;
}

/* ORB (heartbeat sync) */
.orb {
  position: absolute;
  width: 200px;
  height: 200px;
  background: radial-gradient(circle, rgba(59,130,246,0.35), transparent);
  border-radius: 999px;
  filter: blur(50px);

  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

  animation: heartbeat 3s ease-in-out infinite;
}

/* BOX */
.box {
  width: 100px;
  height: 100px;

  background: rgba(255,255,255,0.06);
  backdrop-filter: blur(25px);
  border-radius: 24px;

  display: flex;
  align-items: center;
  justify-content: center;

  margin: auto;
  position: relative;
  z-index: 2;

  box-shadow: 0 25px 80px rgba(0,0,0,0.5);

  animation: floatBox 4s ease-in-out infinite;
}

@media (min-width: 768px) {
  .box {
    width: 130px;
    height: 130px;
  }
}

/* ICON */
.icon {
  width: 32px;
  height: 32px;
  color: white;
}

@media (min-width: 768px) {
  .icon {
    width: 42px;
    height: 42px;
  }
}

/* RINGS (sync heartbeat) */
.ring {
  position: absolute;
  border-radius: 999px;
  border: 1px solid rgba(96,165,250,0.2);

  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.r1 { width: 140px; height: 140px; animation: pulse 3s infinite; }
.r2 { width: 200px; height: 200px; animation: pulse 3s infinite 1s; }
.r3 { width: 260px; height: 260px; animation: pulse 3s infinite 2s; }

/* TEXT */
.title {
  font-family: 'Playfair Display', serif;
  @apply text-2xl md:text-5xl text-white;
}

.highlight {
  font-family: 'Playfair Display', serif;
  @apply text-2xl md:text-5xl italic text-blue-400 mt-2;
}

.sub {
  @apply text-xs md:text-sm text-blue-300 mt-5;
}

/* BUTTON (CLICK SAFE) */
.btn {
  @apply mt-10 px-6 py-3 rounded-full bg-white/10 backdrop-blur border border-white/20 text-white transition;

  position: relative;
  z-index: 20;
}

.btn:hover {
  transform: scale(1.05);
  background: rgba(255,255,255,0.2);
}

/* FADE */
.fade1 { animation: fadeUp 1s forwards 0.5s; opacity:0 }
.fade2 { animation: fadeUp 1s forwards 1.3s; opacity:0 }
.fade3 { animation: fadeUp 1s forwards 2.2s; opacity:0 }
.fade4 { animation: fadeUp 1s forwards 3s; opacity:0 }

/* ANIMATIONS */
@keyframes fadeUp {
  from { opacity:0; transform: translateY(20px); }
  to { opacity:1; transform: translateY(0); }
}

/* heartbeat (smooth) */
@keyframes heartbeat {
  0%,100% { transform: translate(-50%, -50%) scale(1); }
  50% { transform: translate(-50%, -50%) scale(1.1); }
}

@keyframes pulse {
  0% { transform: translate(-50%, -50%) scale(0.7); opacity:0.4 }
  100% { transform: translate(-50%, -50%) scale(1.6); opacity:0 }
}

@keyframes floatUp {
  from { transform: translateY(0); }
  to { transform: translateY(-120vh); opacity:0 }
}

@keyframes floatBox {
  0%,100% { transform: translateY(0); }
  50% { transform: translateY(-8px); }
}

</style>