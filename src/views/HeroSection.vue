<template>
  <section>
    <div class="hero-section">
      <div class="video-container">
        <iframe
          ref="videoElement"
          class="hero-video"
          src="https://www.youtube.com/embed/EngW7tLk6R8?autoplay=1&mute=1&loop=1&playlist=EngW7tLk6R8&controls=0&showinfo=0&rel=0&modestbranding=1&playsinline=1"
          frameborder="0"
          allow="autoplay; encrypted-media"
          allowfullscreen
        ></iframe>
      </div>

      <div class="hero-overlay"></div>

      <div class="hero-content">
        <h1 class="hero-title">
          Excellence, Equity,<br />
          and Opportunity
        </h1>
      </div>

      <button class="play-control" @click="togglePlayback">
        <span class="control-text">{{ isPlaying ? 'Pause Video' : 'Play Video' }}</span>
        <span class="control-icon">
          <svg
            v-if="!isPlaying"
            width="20"
            height="20"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
          >
            <polygon points="5 3 19 12 5 21 5 3"></polygon>
          </svg>
          <svg
            v-else
            width="20"
            height="20"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
          >
            <rect x="6" y="4" width="4" height="16"></rect>
            <rect x="14" y="4" width="4" height="16"></rect>
          </svg>
        </span>
      </button>
    </div>

    <section class="whats-happening">
      <div class="container">
        <small class="section-title">What's Happening at FCPS</small>
        <div class="cards-grid">
          <div class="card">
            <p class="card-title">Future Ready Index</p>
            <small class="card-description">
              View data showing how FCPS prepares every student for the future.
            </small>
          </div>

          <div class="card">
            <p class="card-title">Budget Story: Every Success Has A Story</p>
            <small class="card-description">
              Learn about how student success starts with a strong budget.
            </small>
          </div>

          <div class="card">
            <p class="card-title">Comprehensive Boundary Review</p>
            <small class="card-description">
              Explore draft boundary scenarios in the Boundary Explorer Tool.
            </small>
          </div>

          <div class="card">
            <p class="card-title">Weather Cancellation Procedures</p>
            <small class="card-description">
              Be informed in the case of inclement weather or other disruptions.
            </small>
          </div>
        </div>
      </div>
    </section>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const videoElement = ref(null)
const isPlaying = ref(true)

const togglePlayback = () => {
  const iframe = videoElement.value
  if (iframe) {
    const message = isPlaying.value ? '{"event":"command","func":"pauseVideo","args":""}' : '{"event":"command","func":"playVideo","args":""}'
    iframe.contentWindow.postMessage(message, '*')
    isPlaying.value = !isPlaying.value
  }
}

onMounted(() => {
  // Enable YouTube API
  const iframe = videoElement.value
  if (iframe) {
    iframe.src += '&enablejsapi=1'
  }
})
</script>

<style scoped>
.hero-section {
  position: relative;
  width: 100%;
  height: 100vh;
  min-height: 500px;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding-bottom: 100px;
}

.video-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
}

.hero-video {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 100vw;
  height: 56.25vw;
  min-height: 100vh;
  min-width: 177.77vh;
  transform: translate(-50%, -50%);
  pointer-events: none;
  z-index: 1;
}

.hero-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(to right, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.2));
  z-index: 2;
}

.hero-content {
  position: absolute;
  z-index: 3;
  bottom: -10px;
  padding: 0px 60px 0;
  max-width: 1400px;
  margin: 50px auto 150px;
}

.hero-title {
  font-weight: 700;
  line-height: 1.2;
  color: #ffffff;
  margin: 0;
  text-align: left;
  text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.5);
  font-size: 3.5rem;
}

.play-control {
  position: absolute;
  bottom: 30px;
  right: 30px;
  z-index: 4;
  display: flex;
  align-items: center;
  gap: 10px;
  background: transparent;
  border: none !important;
  font-family: 'Open Sans', sans-serif;
  color: #ffffff;
  padding: 12px 20px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 600;
  transition: all 0.3s ease;
}

.play-control:hover {
  opacity: 0.8;
}

.play-control:active {
  transform: translateY(0);
}

.control-text {
  display: inline-block;
}

.control-icon {
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Responsive Design */
@media (max-width: 768px) {
  .hero-content {
    padding: 0 30px;
  }

  .hero-title {
    font-size: 36px;
  }

  .play-control {
    bottom: 20px;
    right: 20px;
    padding: 10px 16px;
    font-size: 13px;
  }

  .control-text {
    display: none;
  }
}

@media (max-width: 480px) {
  .hero-title {
    font-size: 28px;
  }
}

section {
  position: relative;
}

.whats-happening {
  background-color: #0d5e6d;
  position: absolute;
  top: 100%;
  right: 0;
  transform: translate(0%, -50%);
  z-index: 10;
  max-width: 1440px;
  padding: 2rem 4rem;
  color: white;
}

.container {
  margin: 0 auto;
}

.section-title {
  font-size: 0.9rem;
  font-weight: 600;
  letter-spacing: 0.5px;
  text-transform: none;
}

.cards-grid {
  display: flex;
  gap: 0;
  align-items: stretch;
  margin-top: 1.5rem;
}

.card {
  flex: 1;
  padding: 0 1.5rem;
  min-width: 0;
  border-left: #ffb500 solid 2px;
  cursor: pointer;
  transition: color 0.3s ease;
}

.card-title {
  font-size: 1rem;
  font-weight: 700;
  margin: 0 0 0.7rem 0;
  line-height: 1.4;
}

.card-description {
  font-size: 0.875rem;
  line-height: 1.5;
  margin: 0;
  font-weight: 600;
  opacity: 0.95;
}

.card:hover {
  color: #ffb500;
}

/* Responsive Design */
@media (max-width: 1024px) {
  .cards-grid {
    flex-wrap: wrap;
  }

  .card {
    flex-basis: calc(50% - 0.75rem);
    padding: 1rem;
    margin-bottom: 1.5rem;
  }
}

@media (max-width: 640px) {
  .cards-grid {
    flex-direction: column;
    gap: 1.5rem;
  }

  section {
    height: fit-content;
  }

  .card,
  .section-title {
    flex-basis: auto;
    padding: 0 1.5rem;
  }

  .hero-content {
    margin: 50px auto;
  }

  .whats-happening {
    position: static;
    padding: 2rem 0rem;
    top: 0;
    right: 0;
    transform: translate(0%, 0%);
  }
}
</style>
