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
    </div>

    <!-- 💎 content -->
    <div class="container">

      <!-- 🔥 typography premium -->
      <h1 class="title">
        for adee
      </h1>

      <p class="subtitle">
        something small... but special 💙
      </p>

      <!-- 🔘 PIN -->
      <div class="pin-display">
        <span v-for="i in 6" :key="i" class="dot">
          <span v-if="pin.length >= i" class="filled"></span>
        </span>
      </div>

      <!-- 🔢 KEYPAD -->
      <div class="keypad">
        <button v-for="n in numbers" :key="n" @click="press(n)">
          {{ n }}
        </button>

        <button class="empty"></button>
        <button @click="press(0)">0</button>
        <button @click="del">⌫</button>
      </div>

      <!-- ❌ error -->
      <p v-if="error" class="error">
        hmm salah 😭 coba lagi yaa
      </p>

    </div>

  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

const emit = defineEmits(['success'])

const pin = ref("")
const error = ref(false)

const numbers = [1,2,3,4,5,6,7,8,9]

const press = (num) => {
  if (pin.value.length < 6) pin.value += num
}

const del = () => {
  pin.value = pin.value.slice(0, -1)
}

watch(pin, (val) => {
  if (val.length === 6) {
    if (val === "160408") {
      error.value = false
      setTimeout(() => emit('success'), 400)
    } else {
      error.value = true
      setTimeout(() => {
        pin.value = ""
        error.value = false
      }, 600)
    }
  }
})

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
  top: -150px;
  left: -150px;
}

.g2 {
  width: 400px;
  height: 400px;
  background: #60a5fa;
  bottom: -150px;
  right: -150px;
}

@keyframes moveGlow {
  from { transform: translateY(0); }
  to { transform: translateY(30px); }
}

/* ✨ floating */
.floating span {
  position: absolute;
  bottom: -10px;
  font-size: 14px;
  opacity: 0.15;
  animation: floatUp linear infinite;
}

@keyframes floatUp {
  from { transform: translateY(0); }
  to { transform: translateY(-120vh); opacity: 0; }
}

/* 💎 content */
.container {
  @apply text-center z-10 px-6;
}

/* 🔥 typography */
.title {
  font-family: 'Playfair Display', serif;
  @apply text-4xl md:text-5xl text-white font-semibold;
}

.subtitle {
  font-family: 'Inter', sans-serif;
  @apply text-sm text-blue-300 mt-2;
}

/* 🔘 PIN */
.pin-display {
  @apply flex justify-center gap-3 mt-8 mb-6;
}

.dot {
  @apply w-4 h-4 rounded-full border border-blue-400/50 flex items-center justify-center;
}

.filled {
  @apply w-2.5 h-2.5 bg-blue-400 rounded-full;
  animation: pop 0.2s ease;
}

@keyframes pop {
  from { transform: scale(0.5); }
  to { transform: scale(1); }
}

/* 🔢 keypad */
.keypad {
  @apply grid grid-cols-3 gap-4 max-w-xs mx-auto;
}

.keypad button {
  @apply w-16 h-16 rounded-full bg-white/10 backdrop-blur border border-white/20 text-white text-lg transition;
}

.keypad button:hover {
  transform: scale(1.08);
  box-shadow: 0 0 20px rgba(59,130,246,0.3);
}

.keypad button:active {
  transform: scale(0.9);
}

.empty {
  visibility: hidden;
}

/* ❌ error */
.error {
  @apply text-red-400 text-sm mt-4;
  animation: shake 0.3s;
}

@keyframes shake {
  0% { transform: translateX(0); }
  25% { transform: translateX(-4px); }
  50% { transform: translateX(4px); }
  75% { transform: translateX(-4px); }
  100% { transform: translateX(0); }
}

</style>