<template>
  <main>
    <section class="fcps-stats-section">
      <div class="stats-container">
        <!-- Left Column - Mission Statement -->
        <div class="mission-column">
          <div class="mission-content">
            <h2 class="mission-text">
              Fairfax County Public Schools inspires and empowers students to meet high academic standards.
            </h2>
            <button class="cta-button">
              More About FCPS
              <svg class="arrow-icon" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd" />
              </svg>
            </button>
          </div>
        </div>

        <!-- Right Column - Stats Grid -->
        <div class="stats-grid">
          <!-- Stat Card 1 - Orange -->
          <div class="stat-card stat-card-orange">
            <div class="stat-overlay"></div>
            <div class="stat-content">
              <p class="stat-text">
                We're the 9th largest school system in the U.S. — 199 schools
              </p>
            </div>
          </div>

          <!-- Stat Card 2 - Teal -->
          <div class="stat-card stat-card-teal">
            <div class="stat-overlay"></div>
            <div class="stat-content">
              <p class="stat-text">
                We teach nearly 183,000 enrolled students
              </p>
            </div>
          </div>

          <!-- Stat Card 3 - Dark Teal -->
          <div class="stat-card stat-card-dark-teal">
            <div class="stat-overlay"></div>
            <div class="stat-content">
              <p class="stat-text">
                FCPS employs over 25,000 full-time staff
              </p>
            </div>
          </div>

          <!-- Stat Card 4 - Yellow -->
          <div class="stat-card stat-card-yellow">
            <div class="stat-overlay"></div>
            <div class="stat-content">
              <p class="stat-text" style="color: black;">
                Our school bus fleet is the largest in the country — over 1,600 buses
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script setup>
// Component now uses Composition API with <script setup>
// No reactive state needed for this presentational component
</script>

<style scoped>
.fcps-stats-section {
  width: 100%;
  padding: 0;
}

.stats-container {
  display: flex;
  width: 100%;
  min-height: 500px;
}

/* Left Column - Mission Statement */
.mission-column {
  flex: 0 0 45%;
  background-color: #e8e8e8;
  display: flex;
  align-items: center;
  justify-content: left;
  padding: 60px 20px;
}

.mission-content {
  max-width: 500px;
}

.mission-text {
  font-size: 28px;
  line-height: 1.4;
  color: #333;
  margin: 0 0 30px 0;
  font-weight: 400;
}

.cta-button {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background-color: #0f6e7e;
  color: white;
  border: none;
  padding: 14px 24px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.3s ease;
  border-radius: 4px;
}

.cta-button:hover {
  background-color: #0d5d6b;
}

.arrow-icon {
  width: 20px;
  height: 20px;
}

/* Right Column - Stats Grid */
.stats-grid {
  flex: 0 0 55%;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(2, 1fr);
}

/* Added smooth zoom effect on hover */
.stat-card {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 40px 30px;
  background-size: 110%;
  background-position: center;
  background-repeat: no-repeat;
  overflow: hidden;
  min-height: 250px;
  transition: background-size 0.5s ease-in-out;
}

.stat-card:hover {
  background-size: 130%;
}

/* Placeholder background images */
.stat-card-orange {
  background-image: url('/pic1.png?height=400&width=400');
}

.stat-card-teal {
  background-image: url('/pic1.png?height=400&width=400');
}

.stat-card-dark-teal {
  background-image: url('/pic1.png?height=400&width=400');
}

.stat-card-yellow {
  background-image: url('/pic1.png?height=400&width=400');
    color: #000 !important;
}

/* Color overlays */
.stat-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  opacity: 0.85;
  z-index: 1;
}

.stat-card-orange .stat-overlay {
  background-color: #D3451E;
}

.stat-card-teal .stat-overlay {
  background-color: #00657F;
}

.stat-card-dark-teal .stat-overlay {
  background-color: #00657F;
}

.stat-card-yellow .stat-overlay {
  background-color: #FFC843;

}

.stat-content {
  position: relative;
  z-index: 2;
  text-align: center;
}

.stat-text {
  font-size: 22px;
  line-height: 1.5;
  color: white;
  margin: 0;
  font-weight: 500;
  text-shadow: 0 1px 3px rgba(0, 0, 0, 0.2);
}

/* Responsive Design */
@media (max-width: 1024px) {
  .stats-container {
    flex-direction: column;
  }

  .mission-column,
  .stats-grid {
    flex: 1 1 100%;
  }

  .mission-column {
    min-height: 400px;
  }

  .mission-text {
    font-size: 24px;
  }
}

@media (max-width: 768px) {
  .stats-grid {
    grid-template-columns: 1fr;
    grid-template-rows: repeat(4, 1fr);
  }

  .stat-card {
    min-height: 200px;
    padding: 30px 20px;
  }

  .stat-text {
    font-size: 18px;
  }

  .mission-text {
    font-size: 22px;
  }

  .mission-column {
    padding: 40px 30px;
  }
}
</style>
