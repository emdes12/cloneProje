<template>
  <div class="event-component">
    <!-- Header Section -->
    <div class="event-header">
      <h2 class="event-title">Upcoming Events</h2>
      <PryButton btnText="See More Events" />
    </div>

    <!-- Calendar Controls -->
    <div class="calendar-controls">
      <div class="view-controls">
        <div class="date-navigation">
          <span class="today-label" @click="goToToday">Today</span>
          <button class="nav-button" @click="goToPreviousWeek">
            <ChevronLeft :size="14" />
          </button>
          <div class="date-display">
            <h3 class="date-range">{{ dateRange }}</h3>
          </div>
          <button class="nav-button" @click="goToNextWeek">
            <ChevronRight :size="14" />
          </button>
        </div>

        <div class="view-toggle">
          <button
            class="toggle-btn"
            :class="{ active: currentView === 'month' }"
            @click="currentView = 'month'"
          >
            Month
          </button>
          <button
            class="toggle-btn"
            :class="{ active: currentView === 'week' }"
            @click="currentView = 'week'"
          >
            Week
          </button>
          <button
            class="toggle-btn"
            :class="{ active: currentView === 'day' }"
            @click="currentView = 'day'"
          >
            Day
          </button>
        </div>
      </div>

      <div class="right-controls">
        <div class="search-box">
          <Search :size="18" class="search-icon" />
          <input type="text" placeholder="Search" v-model="searchQuery" class="search-input" />
          <Filter :size="18" class="filter-icon" />
        </div>
        <button class="subscribe-btn">Subscribe</button>
      </div>
    </div>

    <!-- Filter Section -->
    <div class="filter-section" v-if="selectedFilter">
      <div class="filter-tag">
        <span>Filter:</span>
        <div class="filter-badge">
          <House :size="14" />
          <span>{{ selectedFilter }}</span>
          <button @click="clearFilter" class="clear-filter">
            <X :size="14" />
          </button>
        </div>
      </div>
    </div>

    <!-- Calendar Grid -->
    <div class="calendar-container" :class="`view-${currentView}`">
      <!-- Desktop Calendar View -->
      <div v-if="!isMobile" class="calendar-grid">
        <!-- Days Header -->
        <div class="calendar-header">
          <div v-for="day in daysOfWeek" :key="day" class="day-header">
            {{ day }}
          </div>
        </div>

        <!-- Calendar Body -->
        <div class="calendar-body">
          <div
            v-for="day in calendarDays"
            :key="day.date"
            class="calendar-day"
            :class="{
              'has-events': day.events.length > 0,
              'is-today': isToday(day.date),
            }"
          >
            <div class="day-number">
              {{ day.day }}
              <Sun v-if="day.weather === 'sunny'" :size="16" class="weather-icon" />
            </div>
            <div class="day-events">
              <div
                v-for="event in day.events"
                :key="event.id"
                class="event-item"
                @click="openEventDetails(event)"
              >
                {{ event.title }}
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Mobile Calendar View -->
      <div v-else class="mobile-calendar">
        <div class="mobile-days-header">
          <div v-for="day in calendarDays" :key="day.date" class="mobile-day-column">
            <div class="mobile-day-name">{{ getDayName(day.date) }}</div>
            <div class="mobile-day-number" :class="{ 'is-today': isToday(day.date) }">
              {{ day.day }}
              <Sun v-if="day.weather === 'sunny'" :size="12" class="weather-icon" />
            </div>
            <div class="mobile-events">
              <div
                v-for="event in day.events"
                :key="event.id"
                class="mobile-event-item"
                @click="openEventDetails(event)"
              >
                {{ event.title }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { ChevronLeft, ChevronRight, Search, Filter, House, X, Sun } from 'lucide-vue-next'
import PryButton from './PryButton.vue'

// State
const currentView = ref('week')
const currentWeek = ref(new Date(2025, 11, 8))
const searchQuery = ref('')
const selectedFilter = ref('Central Office')
const isMobile = ref(false)

// Sample events data
const events = ref([
  {
    id: 1,
    date: '2025-12-09',
    title: "Superintendent's Community Conversations",
    location: 'Central Office',
  },
  {
    id: 2,
    date: '2025-12-10',
    title: 'Toilet Training',
    location: 'Central Office',
  },
  {
    id: 3,
    date: '2025-12-10',
    title: 'Toilet Training',
    location: 'Central Office',
  },
  {
    id: 4,
    date: '2025-12-11',
    title: 'Special Education Teacher - Virtual Information Session',
    location: 'Central Office',
  },
  {
    id: 5,
    date: '2025-12-12',
    title: "Superintendent's Community Conversations",
    location: 'Central Office',
  },
  {
    id: 6,
    date: '2025-12-13',
    title: 'Co-Parenting: Two Parents, Two Homes',
    location: 'Central Office',
  },
])

// Days of week
const daysOfWeek = ['SUNDAY', 'MONDAY', 'TUESDAY', 'WEDNESDAY', 'THURSDAY', 'FRIDAY', 'SATURDAY']

// Computed
const dateRange = computed(() => {
  const startDate = new Date(currentWeek.value)
  const endDate = new Date(currentWeek.value)
  endDate.setDate(endDate.getDate() + 6)

  const options = { month: 'short', day: 'numeric' }
  const start = startDate.toLocaleDateString('en-US', options)
  const end = endDate.toLocaleDateString('en-US', options)
  const year = startDate.getFullYear()

  return `${start}-${end} ${year}`
})

const calendarDays = computed(() => {
  const days = []
  const startDate = new Date(currentWeek.value)

  for (let i = 0; i < 7; i++) {
    const date = new Date(startDate)
    date.setDate(date.getDate() + i)
    const dateString = date.toISOString().split('T')[0]

    days.push({
      date: dateString,
      day: date.getDate() - 1,
      events: events.value.filter((e) => e.date === dateString),
      weather: i === 2 ? 'sunny' : null,
    })
  }

  return days
})

// Methods
const goToToday = () => {
  currentWeek.value = new Date()
}

const goToPreviousWeek = () => {
  const newDate = new Date(currentWeek.value)
  newDate.setDate(newDate.getDate() - 7)
  currentWeek.value = newDate
}

const goToNextWeek = () => {
  const newDate = new Date(currentWeek.value)
  newDate.setDate(newDate.getDate() + 7)
  currentWeek.value = newDate
}

const isToday = (dateString) => {
  const today = new Date().toISOString().split('T')[0]
  console.log('getday:', {
    'argu': dateString,
    'dayScrip': today,
    'anwser': dateString === today,
  })
  return dateString === today
}

const getDayName = (dateString) => {
  const date = new Date(dateString)
  return date.toLocaleDateString('en-US', { weekday: 'short' }).toUpperCase()
}

const clearFilter = () => {
  selectedFilter.value = null
}

const openEventDetails = (event) => {
  console.log('Event clicked:', event)
  // Handle event click - open modal or navigate
}

const checkMobile = () => {
  isMobile.value = window.innerWidth <= 768
}

// Lifecycle
onMounted(() => {
  checkMobile()
  window.addEventListener('resize', checkMobile)
})

onUnmounted(() => {
  window.removeEventListener('resize', checkMobile)
})
</script>

<style scoped>
.event-component {
  max-width: 100%;
  font-family: 'Open Sans', sans-serif;
}

/* Header */
.event-header {
  text-align: center;
  margin-bottom: 30px;
  display: grid;
  place-items: center;
}

.event-title {
  color: #00566b;
  font-size: 32px;
  font-weight: 700;
  margin: 0 0 20px 0;
}

/* Calendar Controls */
.calendar-controls {
  margin-bottom: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 15px;
}

.date-navigation {
  display: flex;
  align-items: center;
  gap: 5px;
}

.nav-button {
  background: none;
  border: none;
  cursor: pointer;
  color: #00566b;
  padding: 5px;
  display: flex;
  align-items: center;
  transition: color 0.3s;
}

.nav-button:hover {
  color: #ffb500;
}

.date-display {
  display: flex;
  align-items: center;
  gap: 5px;
}

.today-label {
  padding: 5px 12px;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.today-label:hover {
  background-color: #e0e0e0;
}

.date-range {
  color: #00566b;
  font-size: 18px;
  font-weight: 600;
  margin: 0;
}

.view-controls {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: 10px;
}

.view-toggle {
  display: flex;
  gap: 5;
  border-radius: 4px;
  overflow: hidden;
}

.toggle-btn {
  background: white;
  border: none;
  color: #00566b;
  cursor: pointer;
  font-size: 14px;
  font-weight: 500;
  transition: all 0.3s;
}


.toggle-btn.active {
  border-bottom: 1px solid #00566b;
}


.right-controls {
  display: flex;
  gap: 10px;
  align-items: center;
}

.search-box {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
  background: white;
}

.search-icon,
.filter-icon {
  color: #666;
}

.search-input {
  border: none;
  outline: none;
  font-size: 14px;
  min-width: 150px;
}

.subscribe-btn {
  padding: 8px 16px;
  background-color: #666;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 500;
  transition: background-color 0.3s;
}

.subscribe-btn:hover {
  background-color: #555;
}

/* Filter Section */
.filter-section {
  width: 100%;
  background-color: #cbcccc;
  padding: 3px 8px;
  margin-bottom: 20px;
}

.filter-tag {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 14px;
}

.filter-badge {
  display: flex;
  align-items: center;
  gap: 4px;
  padding: 6px 12px;
  border-radius: 20px;
  color: #00566b;
}

.clear-filter {
  background: none;
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  color: #00566b;
  padding: 0;
  margin-left: 4px;
}

.clear-filter:hover {
  color: #ffb500;
}

/* Calendar Grid - Desktop */
.calendar-grid {
  overflow: hidden;
}

.calendar-header {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  background-color: #f8f8f8;
  border-bottom: 1px solid #ddd;
}

.day-header {
  padding: 12px;
  text-align: center;
  font-size: 12px;
  font-weight: 600;
  color: #00566b;
}

.calendar-body {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  min-height: 400px;
}

.calendar-day {
  border-right: 1px solid #eee;
  border-bottom: 1px solid #eee;
  padding: 10px;
  min-height: 120px;
  background: white;
  transition: background-color 0.3s;
}

.calendar-day:nth-child(7n) {
  border-right: none;
}

.calendar-day:hover {
  background-color: #f9f9f9;
}

.day-number {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-weight: 600;
  color: #00566b;
  margin-bottom: 8px;
  font-size: 14px;
}

.is-today .day-number {
  color: #ffb500;
}

.weather-icon {
  color: #ffb500;
}

.day-events {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.event-item {
  padding: 6px 8px;
  border-radius: 4px;
  font-size: 12px;
  color: #00566b;
  cursor: pointer;
  transition: background-color 0.3s;
  line-height: 1.4;
}

.event-item:hover {
  background-color: #d0e8ed;
}

/* Mobile Calendar */
.mobile-calendar {
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
}

.mobile-days-header {
  display: flex;
  min-width: 100%;
  padding-bottom: 10px;
}

.mobile-day-column {
  flex: 0 0 auto;
  min-width: 100px;
  border-right: 1px solid #ddd;
  overflow: hidden;
  background: white;
}

.mobile-day-name {
  background-color: #f8f8f8;
  padding: 8px;
  text-align: center;
  font-size: 11px;
  font-weight: 600;
  color: #00566b;
  border-bottom: 1px solid #ddd;
}

.mobile-day-number {
  padding: 8px;
  text-align: center;
  font-weight: 600;
  color: #00566b;
  font-size: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 4px;
  border-bottom: 1px solid #eee;
}

.mobile-day-number.is-today {
  color: #ffb500;
}

.mobile-events {
  padding: 8px;
  display: flex;
  flex-direction: column;
  gap: 6px;
  min-height: 100px;
}

.mobile-event-item {
  background-color: #e8f4f7;
  padding: 6px;
  border-radius: 4px;
  font-size: 11px;
  color: #00566b;
  cursor: pointer;
  line-height: 1.3;
}

/* Responsive */
@media (max-width: 768px) {
  .event-component {
    padding: 15px;
  }

  .event-title {
    font-size: 24px;
  }

  .date-range {
    font-size: 18px;
  }

  .view-controls {
    flex-direction: column;
    align-items: stretch;
  }

  .right-controls {
    flex-direction: column;
    width: 100%;
  }

  .search-box {
    width: 100%;
  }

  .search-input {
    width: 100%;
  }

  .subscribe-btn {
    width: 100%;
  }
}
</style>
