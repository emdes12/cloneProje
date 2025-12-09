<script setup>
import PryButton from '../components/PryButton.vue'
import VideoSection from '@/components/VideoSection.vue'
import EventSection from '@/components/EventSection.vue';
import HowTo from '@/components/HowTo.vue';
import FooterSection from '@/components/FooterSection.vue';
</script>

<template>
  <main class="container">
    <!-- Actions/Review -->
    <div>
      <div class="top">
        <div>
          <h1>FCPS on the Move</h1>
          <span>
            These videos showcase our amazing students--and the staff that help make Fairfax County
            Public Schools a nationally recognized school division.
          </span>
        </div>

        <div class="non">
          <PryButton btnText="Stories on youtube" />
        </div>
      </div>

      <VideoSection />

      <EventSection />

      <HowTo />
    </div>
  </main>

  <FooterSection />
</template>

<style scoped>
.top {
  display: flex;
  align-items: start;
  justify-content: space-between;
  gap: 30px;
}

.top h1 {
  font-weight: 700;
  font-size: 32px;
  color: #00566b;
}

.top span {
  font-family: 'Open Sans';
  font-weight: 400;
  font-size: 16px;
}

@media (max-width: 750px) {
  .non {
    display: none;
  }

  .top h1 {
    font-size: 27px;
  }
}
</style>
