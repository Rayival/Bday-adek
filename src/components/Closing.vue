<template>
  <div class="wrapper">

    <!-- 🌌 bg -->
    <div class="bg"></div>

    <!-- 🌫️ glow -->
    <div class="glow"></div>

    <!-- 🌙 moon -->
    <div class="moon"></div>

    <!-- ✨ stars -->
    <div class="stars">
      <span v-for="i in 25" :key="i" :style="randomStar()"></span>
    </div>

    <!-- 🌠 shooting -->
    <div class="shooting"></div>

    <!-- 🌸 flowers -->
    <div class="flowers">
      <span v-for="i in 5" :key="'f'+i" :style="randomFlower()">🌸</span>
    </div>

    <!-- 💙 love -->
    <div class="love">
      <span v-for="i in 6" :key="'l'+i" :style="randomLove()">💙</span>
    </div>

    <!-- 💎 content -->
    <div class="content">

      <div class="text-box">

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
          more than i ever said...
        </p>

        <p class="sub fade5">
          semoga hari-hari kamu selalu baik ✨
        </p>

        <p class="final fade6">
          take care... always 🌙
        </p>

      </div>

    </div>

  </div>
</template>

<script setup>
const randomStar = () => ({
  left: Math.random() * 100 + "%",
  top: Math.random() * 100 + "%",
  animationDuration: 2 + Math.random() * 4 + "s"
})

const randomFlower = () => ({
  left: Math.random() * 100 + "%",
  animationDelay: Math.random() * 2 + "s"
})

const randomLove = () => ({
  left: Math.random() * 100 + "%",
  animationDuration: 6 + Math.random() * 5 + "s"
})
</script>

<style scoped>

/* wrapper */
.wrapper {
  @apply relative flex items-center justify-center overflow-hidden px-4;
  min-height: 100dvh;
}

/* bg */
.bg {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at center, #0f172a, #020617 70%);
}

/* glow */
.glow {
  position: absolute;
  width: 500px;
  height: 500px;
  background: #3b82f6;
  filter: blur(180px);
  opacity: 0.25;
  border-radius: 999px;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  animation: pulseGlow 6s ease-in-out infinite;
}

/* moon */
.moon {
  position: absolute;
  top: 12%;
  right: 8%;
  width: 90px;
  height: 90px;
  background: radial-gradient(circle, #fff, #93c5fd);
  border-radius: 999px;
  opacity: 0.2;
  filter: blur(3px);
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

/* shooting */
.shooting {
  position: absolute;
  top: 20%;
  left: -10%;
  width: 140px;
  height: 2px;
  background: linear-gradient(to right, white, transparent);
  opacity: 0.6;
  animation: shoot 8s linear infinite;
}

/* flowers */
.flowers span {
  position: absolute;
  bottom: -20px;
  font-size: 18px;
  opacity: 0.6;
  animation: growFlower 3s ease forwards;
}

/* love */
.love span {
  position: absolute;
  bottom: -10px;
  font-size: 16px;
  opacity: 0.2;
  animation: floatLove linear infinite;
}

/* 💎 content */
.content {
  @apply flex items-center justify-center w-full px-4 z-10;
}

/* 💎 TEXT BOX */
.text-box {
  @apply w-full max-w-2xl text-center px-6 md:px-12 py-10 md:py-14 rounded-3xl;

  background: rgba(255,255,255,0.04);
  backdrop-filter: blur(30px);
  border: 1px solid rgba(255,255,255,0.1);

  box-shadow:
    0 30px 120px rgba(0,0,0,0.7),
    inset 0 0 60px rgba(59,130,246,0.08);

  position: relative;
}

/* glow tengah */
.text-box::before {
  content: "";
  position: absolute;
  width: 300px;
  height: 300px;
  background: radial-gradient(circle, rgba(59,130,246,0.15), transparent);
  filter: blur(80px);
  z-index: -1;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}

/* text kecil */
.text {
  font-family: 'Inter', sans-serif;
  @apply text-sm md:text-base text-blue-300 opacity-0 tracking-wide;
}

/* MAIN */
.main {
  font-family: 'Playfair Display', serif;
  @apply text-4xl md:text-6xl text-white mt-6 opacity-0 leading-tight;

  animation:
    glowText 3s ease-in-out infinite alternate,
    pulseText 4s ease infinite;
}

/* sub */
.sub {
  font-family: 'Inter', sans-serif;
  @apply text-sm md:text-base text-blue-400 mt-4 opacity-0;
}

/* final */
.final {
  font-family: 'Caveat', cursive;
  @apply text-xl md:text-2xl text-blue-300 mt-6 opacity-0;
}

/* fade */
.fade1 { animation: fadeIn 1s forwards 0.5s }
.fade2 { animation: fadeIn 1s forwards 1.5s }
.fade3 { animation: fadeIn 1.2s forwards 2.5s }
.fade4 { animation: fadeIn 1s forwards 3.6s }
.fade5 { animation: fadeIn 1s forwards 4.5s }
.fade6 { animation: fadeIn 1.2s forwards 5.5s }

/* anim */
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(12px); }
  to { opacity: 1; transform: translateY(0); }
}

@keyframes blink {
  0%,100% { opacity: 0.2; }
  50% { opacity: 1; }
}

@keyframes growFlower {
  from { transform: translateY(40px) scale(0.5); opacity: 0; }
  to { transform: translateY(0) scale(1); opacity: 0.6; }
}

@keyframes floatLove {
  from { transform: translateY(0); }
  to { transform: translateY(-120vh); opacity: 0; }
}

@keyframes shoot {
  0% { transform: translateX(0); opacity: 0; }
  10% { opacity: 1; }
  100% { transform: translateX(120vw); opacity: 0; }
}

@keyframes pulseGlow {
  0%,100% { transform: translate(-50%, -50%) scale(1); }
  50% { transform: translate(-50%, -50%) scale(1.2); }
}

@keyframes glowText {
  from { text-shadow: 0 0 8px rgba(59,130,246,0.3); }
  to { text-shadow: 0 0 25px rgba(59,130,246,0.7); }
}

@keyframes pulseText {
  0%,100% { transform: scale(1); }
  50% { transform: scale(1.03); }
}

</style>