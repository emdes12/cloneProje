<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const hoveredIndex = ref(null)
const currentIndex = ref(0)
const isMobile = ref(false)

const videosList = ref([
  {
    title: 'TheatreMania 2025',
    link: 'https://www.youtube.com/watch?v=CdGusp2yIkM',
    thumbnail: './072522-4899_0.jpg',
  },
  {
    title: 'How FCPS Delivers Learning: From Warehouse to Classroom',
    link: 'https://www.youtube.com/watch?v=CdGusp2yIkM',
    thumbnail: './092509-2190.jpg',
  },
  {
    title: '32 Years Behind the Wheel: A Day with FCPS Bus Driver Jannell Haskins',
    link: 'https://www.youtube.com/watch?v=CdGusp2yIkM',
    thumbnail: './transcript.00_00_04_11.still001.jpg',
  },
])

const checkMobile = () => {
  isMobile.value = window.innerWidth <= 768
}

const nextVideo = () => {
  if (currentIndex.value < videosList.value.length - 1) {
    currentIndex.value++
  }
}

const prevVideo = () => {
  if (currentIndex.value > 0) {
    currentIndex.value--
  }
}

onMounted(() => {
  checkMobile()
  window.addEventListener('resize', checkMobile)
})

onUnmounted(() => {
  window.removeEventListener('resize', checkMobile)
})
</script>

<template>
  <div class="video-wrapper">
    <div class="video-container">
      <div
        class="video-card"
        v-for="(video, index) in videosList"
        :key="index"
        :class="{
          'is-hovered': hoveredIndex === index,
          'is-first': index === 0 && hoveredIndex === null,
          'is-active': currentIndex === index
        }"
        @mouseenter="hoveredIndex = index"
        @mouseleave="hoveredIndex = null"
      >
        <a :href="video.link" target="_blank" rel="noopener noreferrer">
          <div class="image-wrapper">
            <img :src="video.thumbnail" :alt="video.title" />
            <div class="play-overlay">
              <svg width="64" height="64" viewBox="0 0 64 64" fill="none">
                <circle cx="32" cy="32" r="32" fill="white" fill-opacity="0.9" />
                <path d="M26 20L44 32L26 44V20Z" fill="#00566B" />
              </svg>
            </div>
          </div>
          <p class="video-title">{{ video.title }}</p>
        </a>
      </div>
    </div>

    <!-- Mobile Navigation Buttons -->
    <button
      class="nav-btn prev-btn"
      @click="prevVideo"
      :disabled="currentIndex === 0"
      v-show="isMobile"
    >
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <polyline points="15 18 9 12 15 6"></polyline>
      </svg>
    </button>

    <button
      class="nav-btn next-btn"
      @click="nextVideo"
      :disabled="currentIndex === videosList.length - 1"
      v-show="isMobile"
    >
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <polyline points="9 18 15 12 9 6"></polyline>
      </svg>
    </button>
  </div>
</template>

<style scoped>
.video-wrapper {
  position: relative;
  width: 100%;
}

.video-container {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
  gap: 15px;
  width: 100%;
  transition: grid-template-columns 0.4s ease;
  margin: 20px 0;
}

.video-container:has(.video-card:nth-child(1).is-hovered) {
  grid-template-columns: 2fr 1fr 1fr;
}

.video-container:has(.video-card:nth-child(2).is-hovered) {
  grid-template-columns: 1fr 2fr 1fr;
}

.video-container:has(.video-card:nth-child(3).is-hovered) {
  grid-template-columns: 1fr 1fr 2fr;
}

.video-card {
  position: relative;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.video-card:hover {
  transform: translateY(-5px);
}

.video-card a {
  text-decoration: none;
  display: block;
  height: 100%;
  position: relative;
}

.image-wrapper {
  position: relative;
  width: 100%;
  height: 400px;
  border-radius: 8px;
  overflow: hidden;
}

.image-wrapper img {
  width: 100%;
  height: 400px;
  border-radius: 8px;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.video-card:hover .image-wrapper img {
  transform: scale(1.05);
}

.play-overlay {
  position: absolute;
  top: 0;
  left: 0;
  background-color: #00000075;
  display: grid;
  place-items: center;
  width: 100%;
  height: 100%;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.video-card:hover .play-overlay {
  opacity: 1;
}

.video-title {
  margin: 0;
  padding: 20px 0;
  color: #00566b;
  font-family: 'Open Sans', sans-serif;
  font-size: 18px;
  font-weight: 600;
  line-height: 1.4;
}

.video-title:hover {
  color: #ffb500;
}

.nav-btn {
  display: none;
}

/* Responsive Design */
@media (max-width: 1024px) {
  .video-container {
    grid-template-columns: 1fr 1fr;
  }

  .video-container:has(.video-card:nth-child(1).is-hovered),
  .video-container:has(.video-card:nth-child(2).is-hovered) {
    grid-template-columns: 1fr 1fr;
  }

  .image-wrapper,
  .image-wrapper img {
    height: 300px;
  }
}

@media (max-width: 768px) {
  .video-container {
    display: flex;
    overflow: hidden;
    margin: 20px 0;
  }

  .video-card {
    min-width: 100%;
    transform: translateX(calc(-100% * var(--current-index)));
    transition: transform 0.4s ease, opacity 0.4s ease;
    opacity: 0;
    display: none;
  }

  .video-card.is-active {
    display: block;
    opacity: 1;
  }

  .video-card:hover {
    transform: translateX(calc(-100% * var(--current-index)));
  }

  .image-wrapper,
  .image-wrapper img {
    height: 250px;
  }

  .video-title {
    font-size: 16px;
    padding: 15px 0;
  }

  .nav-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    width: 48px;
    height: 48px;
    background-color: #201f1fe6;
    border: none;
    border-radius: 50%;
    color: #fff;
    cursor: pointer;
    z-index: 10;
    transition: all 0.3s ease;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
  }

  .nav-btn:hover:not(:disabled) {
    background-color: #ffb500;
    transform: translateY(-50%) scale(1.1);
  }

  .nav-btn:disabled {
    opacity: 0.3;
    cursor: not-allowed;
  }

  .prev-btn {
    left: 10px;
  }

  .next-btn {
    right: 10px;
  }

  .nav-btn svg {
    width: 24px;
    height: 24px;
  }
}
</style>
