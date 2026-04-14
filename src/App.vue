<template>
  <!-- 🌌 main scene -->
  <component 
    :is="currentComponent" 
    @next="next" 
    @success="unlock" 
  />

  <!-- 🎧 MUSIC CONTROL -->
  <div class="music-control" @click="toggleMusic">
    <span v-if="isPlaying">🎵</span>
    <span v-else>🔇</span>
  </div>

  <!-- 🎵 AUDIO -->
  <audio ref="audio" loop>
    <source src="@/assets/music/keep-me.mp3" type="audio/mpeg" />
  </audio>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

import LockScreen from './components/LockScreen.vue'
import Intro from './components/Intro.vue'
import Journey from './components/Journey.vue'
import Gallery from './components/Gallery.vue'
import Letter from './components/Letter.vue'
import Closing from './components/Closing.vue'

/* 🔁 navigation */
const page = ref('lock')

const map = {
  lock: LockScreen,
  intro: Intro,
  journey: Journey,
  gallery: Gallery,
  letter: Letter,
  closing: Closing
}

const currentComponent = computed(() => map[page.value])

const unlock = () => page.value = 'intro'

const next = () => {
  const order = ['intro', 'journey', 'gallery', 'letter', 'closing']
  const index = order.indexOf(page.value)
  if (index !== -1 && index < order.length - 1) {
    page.value = order[index + 1]
  }
}

/* 🎧 MUSIC */
const audio = ref(null)
const isPlaying = ref(false)

const toggleMusic = () => {
  if (!audio.value) return

  if (isPlaying.value) {
    audio.value.pause()
    isPlaying.value = false
  } else {
    audio.value.play()
    isPlaying.value = true
  }
}

/* 🎬 auto start (after interaction) */
onMounted(() => {
  const start = () => {
    if (audio.value) {
      audio.value.volume = 0
      audio.value.play().then(() => {
        isPlaying.value = true
        fadeIn()
      }).catch(() => {})
    }
    window.removeEventListener('click', start)
  }

  window.addEventListener('click', start)
})

/* 🔊 smooth volume */
const fadeIn = () => {
  let vol = 0
  const interval = setInterval(() => {
    if (audio.value && vol < 0.3) {
      vol += 0.02
      audio.value.volume = vol
    } else {
      clearInterval(interval)
    }
  }, 100)
}
</script>

<style scoped>

/* 🎧 music button */
.music-control {
  position: fixed;
  bottom: 20px;
  right: 20px;

  width: 52px;
  height: 52px;

  border-radius: 999px;

  background: rgba(255,255,255,0.08);
  backdrop-filter: blur(15px);
  border: 1px solid rgba(255,255,255,0.15);

  display: flex;
  align-items: center;
  justify-content: center;

  font-size: 20px;
  color: white;

  cursor: pointer;

  transition: all 0.3s ease;
  z-index: 999;
}

/* hover */
.music-control:hover {
  transform: scale(1.1);
  box-shadow: 0 0 25px rgba(59,130,246,0.4);
}

/* click */
.music-control:active {
  transform: scale(0.9);
}

/* subtle glow pulse */
.music-control {
  animation: pulseBtn 3s infinite;
}

@keyframes pulseBtn {
  0%,100% { box-shadow: 0 0 0 rgba(59,130,246,0); }
  50% { box-shadow: 0 0 15px rgba(59,130,246,0.4); }
}

</style>