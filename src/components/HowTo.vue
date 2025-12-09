<script setup>
import SecButton from './SecButton.vue';
import PryButton from './PryButton.vue';
</script>

<template>
  <div class="how-section">
    <div class="header">
      <h1>How Do I?</h1>
      <p class="description">
        Explore some of our most frequently asked questions and learn how to take advantage of the many FCPS services available to you.
      </p>
      <SecButton btnText="Contact FCPS" />
    </div>

    <div class="grid-side">
      <div class="button-grid">
        <PryButton btnText="Register my student" />
        <PryButton btnText="Sign up for a newsletter" />
        <PryButton btnText="Find a school" />
        <PryButton btnText="Attend a School Board meeting" />
        <PryButton btnText="Apply for job" />
        <PryButton btnText="Volunteer FCPS" />
        <PryButton btnText="Manage technology tools" />
        <PryButton btnText="Partner with FCPS" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.how-section {
  display: grid;
  grid-template-columns: 440px 1fr;
  width: 100%;
  min-height: 400px;
}

.header {
  background-color: #00566B;
  padding: 60px 40px;
}

h1 {
  color: #FFB500;
  font-size: 36px;
  font-weight: 700;
  margin: 0;
  margin-bottom: 20px;
  font-family: 'Open Sans', sans-serif;
}

.description {
  color: #fff;
  font-size: 16px;
  line-height: 1.6;
  margin: 0;
  margin-bottom: 20px;
  font-family: 'Open Sans', sans-serif;
}

.grid-side {
  background-color: #E2E2E2;
  padding: 60px 80px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.button-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
  width: 100%;
  max-width: 600px;
}

/* Responsive Design */
@media (max-width: 1200px) {
  .how-section {
    grid-template-columns: 380px 1fr;
  }

  .header {
    padding: 50px 30px;
  }

  .grid-side {
    padding: 50px 60px;
  }

  h1 {
    font-size: 32px;
  }

  .description {
    font-size: 15px;
  }
}

@media (max-width: 1024px) {
  .how-section {
    grid-template-columns: 1fr;
  }

  .header {
    padding: 40px 30px;
  }

  .grid-side {
    padding: 40px 30px;
  }

  .button-grid {
    max-width: 100%;
  }
}

@media (max-width: 768px) {
  .header {
    padding: 30px 20px;
  }

  h1 {
    font-size: 28px;
  }

  .description {
    font-size: 14px;
  }

  .grid-side {
    padding: 30px 20px;
  }
}

@media (max-width: 480px) {
  .header {
    padding: 25px 15px;
  }

  h1 {
    font-size: 24px;
  }

  .description {
    font-size: 13px;
  }

  .grid-side {
    padding: 25px 15px;
  }

  .button-grid {
    display: flex;
    gap: 15px;
    flex-wrap: wrap;
  }
}
</style>
