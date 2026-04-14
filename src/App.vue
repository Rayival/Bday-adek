<template>
  <component :is="currentComponent" @next="next" @success="unlock" />
</template>

<script setup>
import { ref, computed } from 'vue'

import LockScreen from './components/LockScreen.vue'
import Intro from './components/Intro.vue'
import Journey from './components/Journey.vue'
import Gallery from './components/Gallery.vue'
import Letter from './components/Letter.vue'
import Closing from './components/Closing.vue'

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
</script>