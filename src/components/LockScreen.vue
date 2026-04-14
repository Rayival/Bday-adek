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

    <!-- 💎 card -->
    <div class="card">

      <!-- 🕒 CLOCK -->
      <div class="header">
        <p class="label">for you 💙</p>
        <h1 class="time">{{ time }}</h1>
        <p class="date">✨ {{ date }}</p>
      </div>

      <!-- ✨ SVG (CLEAN GEOMETRIC, BUKAN ORNAMEN Aneh) -->
      <svg class="svg-line" viewBox="0 0 400 100">
        <path d="M0 50 Q100 0 200 50 T400 50" />
      </svg>

      <!-- 🔘 PIN -->
      <div class="pin-display">
        <span v-for="i in 6" :key="i" class="dot">
          <span v-if="pin.length >= i" class="filled"></span>
        </span>
      </div>

      <!-- 🔢 keypad -->
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
        wrong code 😭 try again yaa
      </p>

    </div>

  </div>
</template>

<script setup>
import { ref, watch, onMounted } from 'vue'

const emit = defineEmits(['success'])

const pin = ref("")
const error = ref(false)

const numbers = [1,2,3,4,5,6,7,8,9]

// ⏰ clock
const time = ref("")
const date = ref("")

onMounted(() => {
  const update = () => {
    const now = new Date()

    time.value = now.toLocaleTimeString('id-ID', {
      hour: '2-digit',
      minute: '2-digit'
    })

    date.value = now.toLocaleDateString('en-US', {
      month: 'long',
      day: 'numeric',
      year: 'numeric'
    })
  }

  update()
  setInterval(update, 1000)
})

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
      setTimeout(() => emit('success'), 500)
    } else {
      error.value = true
      setTimeout(() => {
        pin.value = ""
        error.value = false
      }, 700)
    }
  }
})

const randomStyle = () => ({
  left: Math.random() * 100 + "%",
  animationDuration: 6 + Math.random() * 6 + "s"
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
  background: linear-gradient(120deg, #020617, #0f172a, #020617);
}

/* glow */
.glow {
  position: absolute;
  border-radius: 9999px;
  filter: blur(150px);
  opacity: 0.25;
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

/* floating */
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

/* card */
.card {
  @apply backdrop-blur-xl bg-white/5 border border-white/10
         rounded-3xl p-8 md:p-10 text-center
         shadow-2xl max-w-sm w-full z-10;
}

/* header */
.label {
  @apply text-blue-300 text-sm mb-1;
  letter-spacing: 2px;
}

.time {
  font-family: 'Playfair Display', serif;
  @apply text-5xl text-white;
}

.date {
  @apply text-blue-400 text-sm mt-1;
}

/* SVG line */
.svg-line {
  width: 100%;
  margin: 16px 0;
}

.svg-line path {
  stroke: #60a5fa;
  stroke-width: 1.5;
  fill: none;
  opacity: 0.3;
}

/* PIN */
.pin-display {
  @apply flex justify-center gap-3 mt-6 mb-6;
}

.dot {
  @apply w-4 h-4 rounded-full border border-blue-400/30 flex items-center justify-center;
}

.filled {
  @apply w-2.5 h-2.5 bg-blue-400 rounded-full;
  box-shadow: 0 0 10px rgba(96,165,250,0.6);
}

/* keypad */
.keypad {
  @apply grid grid-cols-3 gap-4 mt-2;
  width: 100%;
  max-width: 260px;
  margin-left: auto;
  margin-right: auto;
}

.keypad button {
  width: 64px;
  height: 64px;

  margin: auto;

  @apply rounded-full bg-white/5 border border-white/10 
         text-white text-lg transition flex items-center justify-center;
}

.keypad button:hover {
  transform: scale(1.1);
  box-shadow: 0 0 20px rgba(59,130,246,0.3);
}

.pin-display {
  @apply flex justify-center gap-3 mt-8 mb-8;
}

.empty {
  opacity: 0;
  pointer-events: none;
}
/* error */
.error {
  @apply text-red-400 text-sm mt-4;
}

</style>