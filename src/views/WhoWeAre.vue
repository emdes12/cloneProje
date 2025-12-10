<template>
  <section class="we-are-fcps">
    <main>
    <div class="container">
      <!-- Header -->
      <div class="section-header">
        <h2 class="section-title">We Are FCPS</h2>
        <a href="#" class="see-more-btn">
          See more FCPS News
          <svg class="arrow-icon" width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M6 12L10 8L6 4" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </a>
      </div>

      <!-- News Cards Grid -->
      <div class="news-grid">
        <!-- Card 1: Superintendent's Weekly Reflections -->
        <article class="news-card">
          <div class="card-image">
            <img src="/pic1.png?height=240&width=400" alt="Superintendent's Weekly Reflections">
          </div>
          <div class="card-content">
            <h3 class="card-title">Superintendent's Weekly Reflections</h3>
            <time class="card-date">DECEMBER 08, 2025</time>
            <p class="card-description">
              Dr. Reid writes about all the great things happening in Fairfax County Public Schools. This week, she visited West Potomac Academy for the launch of an expanded partnership, held a Community Conversation at Churchill Road Elementary School, visited the Mount Vernon High School Holiday Market, and...
            </p>
          </div>
        </article>

        <!-- Card 2: Message from the Superintendent -->
        <article class="news-card card-teal">
          <div class="card-icon-wrapper">
            <div class="envelope-icon">
              <svg width="80" height="60" viewBox="0 0 80 60" fill="none" xmlns="http://www.w3.org/2000/svg">
                <!-- Envelope body -->
                <rect x="5" y="15" width="70" height="45" fill="white" rx="2"/>
                <!-- Orange flap -->
                <path d="M5 15 L40 40 L75 15" fill="#E67E22"/>
                <!-- Envelope outline -->
                <path d="M5 15 L40 40 L75 15 L75 60 L5 60 Z" stroke="white" stroke-width="2" fill="none"/>
              </svg>
            </div>
            <p class="card-icon-label">Message from<br>the Superintendent</p>
          </div>
          <div class="card-content">
            <h3 class="card-title">Message from the Superintendent About Title IX</h3>
            <time class="card-date">DECEMBER 06, 2025</time>
            <p class="card-description">
              View an update on FCPS' efforts to resolve a matter with the U.S. Department of Education (DOE) regarding Title IX.
            </p>
          </div>
        </article>

        <!-- Card 3: AI Lab at Vienna Elementary -->
        <article class="news-card">
          <div class="card-image">
            <img src="/pic2.png?height=240&width=400" alt="AI Lab at Vienna Elementary School">
          </div>
          <div class="card-content">
            <h3 class="card-title">Decoding the Future: AI Lab at Vienna Elementary School Brings Innovative Tech to Students</h3>
            <time class="card-date">DECEMBER 04, 2025</time>
            <p class="card-description">
              At the Vienna.i.Lab, students learn how to better understand and interact with groundbreaking AI technology before entering middle school.
            </p>
          </div>
        </article>
      </div>
    </div>
    </main>
  </section>
</template>

<script setup>
// Component uses Composition API with script setup
</script>

<style scoped>
.we-are-fcps {
  padding: 200px 0px 60px;
  background-color: #fff;

}

.container {
  /* max-width: 1280px; */
  margin: 0 auto;
}

/* Header */
.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 40px;
}

.section-title {
  font-size: 2.5rem;
  font-weight: 700;
  color: #006670;
  margin: 0;
}

.see-more-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 12px 24px;
  background-color: #006670;
  color: white;
  text-decoration: none;
  font-weight: 600;
  font-size: 1rem;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.see-more-btn:hover {
  background-color: #005560;
}

.arrow-icon {
  transition: transform 0.3s ease;
}

.see-more-btn:hover .arrow-icon {
  transform: translateX(4px);
}

/* News Grid */
.news-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  /* gap: 30px; */
}

/* News Card */
.news-card {
  background-color: white;
  overflow: hidden;
  display: flex;
  border: solid 1px #e0e0e0;
  flex-direction: column;
}



.card-image {
  width: 100%;
  height: 240px;
  overflow: hidden;
}

.card-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Teal Card with Icon */
.card-teal {
  color: white;
}

.card-icon-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 60px 20px 40px;
  min-height: 240px;
   background-color: #006670;
}

.envelope-icon {
  margin-bottom: 20px;

}

.card-icon-label {
  font-size: 1.125rem;
  font-weight: 500;
  text-align: center;
  line-height: 1.5;
  margin: 0;
}

/* Card Content */
.card-content {
  padding: 24px;
  flex-grow: 1;
  display: flex;
  flex-direction: column;

}



.card-title {
  font-size: 1.25rem;
  font-weight: 700;
  color: #006670;
  margin: 0 0 12px 0;
  line-height: 1.4;
}



.card-date {
  display: block;
  font-size: 0.875rem;
  font-weight: 700;
  color: #006670;
  margin-bottom: 16px;
  letter-spacing: 0.5px;
}



.card-description {
  font-size: 1rem;
  line-height: 1.6;
  color: #333;
  margin: 0;
}



/* Responsive Design */
@media (max-width: 1024px) {

}

@media (max-width: 768px) {
  .section-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 20px;
    margin-bottom: 30px;
  }

  .section-title {
    font-size: 1.5rem;
  }

  /* .see-more-btn {
    order: 2;
    width: 100%;
    justify-content: center;
    margin-top: 20px;
  } */

  .news-grid {
    grid-template-columns: 1fr;
    gap: 0;
    order: 1;
  }

  /* Mobile card layout - horizontal with thumbnail on left */
  .news-card {
    flex-direction: row;

    border-bottom: 1px solid #e0e0e0;
    box-shadow: none;
    padding: 16px 0;
  }


  /* Small thumbnail on left */
  .card-image {
    width:  100px;
    height: 100px;
    flex-shrink: 0;

    overflow: hidden;
  }

  /* Teal card icon wrapper becomes small thumbnail */
  .card-icon-wrapper {
    width: 100px;
    height: 100px;
    min-height: auto;
    padding: 0;
    flex-shrink: 0;

    background-color: #006670;
  }

  .envelope-icon {
    margin-bottom: 0;
    transform: scale(0.4);
  }

  .card-icon-label {
    /* display: none; */
    font-size: 10px;
  }

  /* Content on right side */
  .card-content {
    padding: 0 0 0 16px;
    background-color: transparent;
  }

  .card-title {
    font-size: 1rem;
    margin-bottom: 6px;
    line-height: 1.3;
  }

  .card-date {
    font-size: 0.75rem;
    margin-bottom: 0;
  }

  /* Hide description on mobile */
  .card-description {
    display: none;
  }

  /* Reorder so button appears after cards */
  .container {
    display: flex;
    flex-direction: column;
  }
}

@media (max-width: 480px) {
  .we-are-fcps {
    padding: 40px 16px;
  }

  .section-title {
    font-size: 1.25rem;
  }

  .card-title {
    font-size: 1rem;
  }
}
</style>
