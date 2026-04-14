<template>
  <div class="wrapper">

    <!-- 🌌 background -->
    <div class="bg"></div>

    <!-- 🌫️ glow -->
    <div class="glow"></div>

    <!-- ✨ stars -->
    <div class="stars">
      <span v-for="i in 25" :key="i" :style="randomStar()"></span>
    </div>

    <!-- 🌸 flowers -->
    <div class="flowers">
      <span v-for="i in 5" :key="'f'+i" :style="randomFlower()">🌸</span>
    </div>

    <!-- 💙 love -->
    <div class="love">
      <span v-for="i in 5" :key="'l'+i" :style="randomLove()">💙</span>
    </div>

    <!-- 💎 content -->
    <div class="content">

      <p class="text fade1">
        i don’t expect anything...
      </p>

      <p class="text fade2">
        i just want you to know...
      </p>

      <h1 class="main fade3">
        you meant a lot to me 💙
      </h1>

      <p class="sub fade4">
        lebih dari yang pernah aku bilang...
      </p>

      <p class="sub fade5">
        semoga hari-hari kamu selalu baik ✨
      </p>

      <p class="final fade6">
        take care... always 🌙
      </p>

    </div>

  </div>
</template>

<script setup>

// ⭐ stars
const randomStar = () => ({
  left: Math.random() * 100 + "%",
  top: Math.random() * 100 + "%",
  animationDuration: 2 + Math.random() * 4 + "s"
})

// 🌸 flowers
const randomFlower = () => ({
  left: Math.random() * 100 + "%",
  animationDelay: Math.random() * 2 + "s"
})

// 💙 love
const randomLove = () => ({
  left: Math.random() * 100 + "%",
  animationDuration: 6 + Math.random() * 5 + "s"
})

</script>

<style scoped>

/* wrapper (SAFE MOBILE) */
.wrapper {
  @apply min-h-screen flex flex-col justify-center items-center relative overflow-hidden px-4;
  padding-top: clamp(80px, 10vh, 140px);
  padding-bottom: clamp(80px, 10vh, 140px);
}

/* background */
.bg {
  position: absolute;
  inset: 0;
  background: linear-gradient(180deg, #020617, #0f172a, #020617);
}

/* glow */
.glow {
  position: absolute;
  width: 400px;
  height: 400px;
  background: #3b82f6;
  filter: blur(150px);
  opacity: 0.2;
  border-radius: 9999px;
  top: 30%;
  left: 50%;
  transform: translateX(-50%);
}

/* stars */
.stars span {
  position: absolute;
  width: 2px;
  height: 2px;
  background: white;
  border-radius: 999px;
  opacity: 0.6;
  animation: blink 3s infinite;
}

/* 🌸 flowers */
.flowers span {
  position: absolute;
  bottom: -20px;
  font-size: 18px;
  opacity: 0.7;
  animation: growFlower 3s ease forwards;
  filter: drop-shadow(0 0 6px rgba(255,255,255,0.3));
}

/* 💙 love */
.love span {
  position: absolute;
  bottom: -10px;
  font-size: 16px;
  opacity: 0.25;
  animation: floatLove linear infinite;
}

/* content */
.content {
  @apply text-center z-10 max-w-xl;
}

/* text kecil */
.text {
  font-family: 'Inter', sans-serif;
  @apply text-sm md:text-base text-blue-300 opacity-0;
}

/* main */
.main {
  font-family: 'Playfair Display', serif;
  @apply text-3xl md:text-5xl text-white mt-6 opacity-0;
}

/* sub */
.sub {
  @apply text-sm text-blue-400 mt-3 opacity-0;
}

/* final */
.final {
  font-family: 'Caveat', cursive;
  @apply text-blue-300 text-lg mt-6 opacity-0;
}

/* fade timing */
.fade1 { animation: fadeIn 1s forwards 0.5s }
.fade2 { animation: fadeIn 1s forwards 1.5s }
.fade3 { animation: fadeIn 1.2s forwards 2.5s }
.fade4 { animation: fadeIn 1s forwards 3.6s }
.fade5 { animation: fadeIn 1s forwards 4.5s }
.fade6 { animation: fadeIn 1.2s forwards 5.5s }

/* animations */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(12px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes blink {
  0%,100% { opacity: 0.2; }
  50% { opacity: 1; }
}

@keyframes growFlower {
  0% {
    transform: translateY(40px) scale(0.5);
    opacity: 0;
  }
  100% {
    transform: translateY(0) scale(1);
    opacity: 0.7;
  }
}

@keyframes floatLove {
  from { transform: translateY(0); }
  to { transform: translateY(-120vh); opacity: 0; }
}

</style>