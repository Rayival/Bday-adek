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
      <span v-for="i in 4" :key="'s'+i" :style="randomStyle()">✨</span>
    </div>

    <!-- 💎 content -->
    <div class="content">

      <h1 class="title">
        little moments ✨
      </h1>

      <p class="subtitle">
        some small memories that still feel special
      </p>

      <!-- 📸 GRID -->
      <div class="grid md:grid-cols-2 gap-6 md:gap-10 mt-12">

        <div
          v-for="(item, i) in items"
          :key="i"
          class="card group"
          :style="{ animationDelay: i * 0.2 + 's' }"
        >

          <!-- 🌟 overlay glow -->
          <div class="overlay"></div>

          <!-- media -->
          <div class="media-wrap">

            <img
              v-if="item.type === 'img'"
              :src="item.src"
              class="media"
            />

            <video
              v-else
              controls
              class="media"
            >
              <source :src="item.src" />
            </video>

          </div>

          <!-- 📝 text -->
          <div class="text">

            <h2 class="card-title">
              {{ item.title }}
            </h2>

            <p class="card-desc">
              {{ item.desc }}
            </p>

          </div>

        </div>

      </div>

      <!-- button -->
      <button @click="$emit('next')" class="btn">
        continue 💙 →
      </button>

    </div>

  </div>
</template>

<script setup>
import foto1 from '@/assets/img/foto1.png'
import foto2 from '@/assets/img/foto2.png'
import video1 from '@/assets/video/video1.png'
import video2 from '@/assets/video/video2.png'

const items = [
  {
    type: 'img',
    src: foto1,
    title: 'that moment',
    desc: 'i don’t know why, but this one feels special.'
  },
  {
    type: 'img',
    src: foto2,
    title: 'simple but nice',
    desc: 'just something small… but it stayed.'
  },
  {
    type: 'video',
    src: video1,
    title: 'a little memory',
    desc: 'this one made me smile, not gonna lie.'
  },
  {
    type: 'video',
    src: video2,
    title: 'still remember',
    desc: 'some moments just don’t fade that easily.'
  }
]

// floating
const randomStyle = () => ({
  left: Math.random() * 100 + "%",
  animationDuration: 6 + Math.random() * 6 + "s"
})
</script>

<style scoped>

/* wrapper */
.wrapper {
  @apply min-h-screen flex flex-col justify-start relative overflow-hidden px-4;
  padding-top: 100px;
  padding-bottom: 100px;
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
  filter: blur(140px);
  opacity: 0.25;
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

/* floating */
.floating span {
  position: absolute;
  bottom: -10px;
  font-size: 14px;
  opacity: 0.2;
  animation: floatUp linear infinite;
}

/* content */
.content {
  @apply text-center z-10 max-w-5xl w-full mx-auto;
}

/* title */
.title {
  font-family: 'Playfair Display', serif;
  @apply text-3xl md:text-5xl text-white font-semibold;
}

.subtitle {
  @apply text-sm md:text-base text-blue-300 mt-3;
}

/* card */
.card {
  @apply relative bg-white/5 backdrop-blur-xl border border-white/10 rounded-2xl overflow-hidden transition duration-500;
  animation: fadeUp 0.8s ease forwards;
}

/* overlay glow */
.overlay {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at center, rgba(59,130,246,0.2), transparent);
  opacity: 0;
  transition: 0.4s;
}

.card:hover .overlay {
  opacity: 1;
}

/* hover */
.card:hover {
  transform: translateY(-10px) scale(1.03);
  box-shadow: 0 25px 80px rgba(0,0,0,0.5);
}

/* media */
.media-wrap {
  overflow: hidden;
}

.media {
  @apply w-full h-[200px] md:h-[260px] object-cover transition duration-500;
}

.card:hover .media {
  transform: scale(1.1);
}

/* text */
.text {
  @apply p-4 text-left;
}

.card-title {
  @apply text-white font-semibold text-lg;
}

.card-desc {
  @apply text-blue-300 text-sm mt-1;
}

/* button */
.btn {
  @apply mt-12 px-6 py-3 rounded-full bg-white/10 backdrop-blur border border-white/20 text-white transition;
}

.btn:hover {
  transform: scale(1.05);
  background: rgba(255,255,255,0.2);
}

/* animasi */
@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(25px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes floatUp {
  from { transform: translateY(0); }
  to { transform: translateY(-120vh); opacity: 0; }
}

</style>