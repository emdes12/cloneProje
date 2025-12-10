<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { Search, ChevronDown, Menu, X, Plus } from 'lucide-vue-next'

// State
const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)
const activeDropdown = ref(null)

// Top navigation items
const topNavItems = [
  { text: 'Families', url: '#' },
  { text: 'Students', url: '#' },
  { text: 'Employees', url: '#' },
  { text: 'Careers', url: '#' },
  { text: 'Community', url: '#' },
  { text: 'Schools', url: '#' },
  { text: 'Superintendent', url: '#' },
  { text: 'School Board', url: '#' }
]

// Main navigation items with dropdowns
const mainNavItems = [
  {
    text: 'About FCPS',
    hasDropdown: true,
    items: ['Mission & Vision', 'Leadership', 'Contact Us']
  },
  {
    text: 'Services',
    hasDropdown: true,
    items: ['Student Services', 'Parent Services', 'Community Services']
  },
  {
    text: 'Academics',
    hasDropdown: true,
    items: ['Curriculum', 'Programs', 'Testing']
  },
  {
    text: 'Get Involved',
    hasDropdown: true,
    items: ['Volunteer', 'PTA', 'Advisory Councils']
  },
  {
    text: 'News and Calendars',
    hasDropdown: true,
    items: ['News', 'Events', 'Calendar']
  }
]

// Methods
const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
  if (isMobileMenuOpen.value) {
    document.body.style.overflow = 'hidden'
  } else {
    document.body.style.overflow = ''
    activeDropdown.value = null
  }
}

const toggleDropdown = (index) => {
  activeDropdown.value = activeDropdown.value === index ? null : index
}

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false
  document.body.style.overflow = ''
  activeDropdown.value = null
}

// Lifecycle
onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  handleScroll()
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  document.body.style.overflow = ''
})
</script>

<template>
  <header class="navbar" :class="{ 'scrolled': isScrolled }">
    <div class="navbar-container">
      <!-- Logo -->
      <a href="/" class="logo-link">
        <img
          src="/fcps-desktop-logo.svg"
          alt="Fairfax County Public Schools"
          class="logo"
          :class="{ 'logo-scrolled': isScrolled }"
        />
      </a>

      <!-- Desktop Navigation -->
      <nav class="desktop-nav">
        <!-- Top Navigation -->
        <div class="top-nav">
          <div class="top-nav-links">
            <a
              v-for="item in topNavItems"
              :key="item.text"
              :href="item.url"
              class="top-nav-link"
            >
              {{ item.text }}
            </a>
          </div>
          <div class="top-nav-actions">
            <button class="language-btn">
              <span class="language-icon">🌐</span>
              English
              <ChevronDown :size="16" />
            </button>
          </div>
        </div>

        <!-- Main Navigation -->
        <div class="main-nav">
          <button class="search-btn" aria-label="Search">
            <Search :size="20" />
          </button>

          <div class="main-nav-links">
            <div
              v-for="(item, index) in mainNavItems"
              :key="item.text"
              class="nav-item"
            >
              <button class="nav-link">
                {{ item.text }}
                <ChevronDown :size="18" v-if="item.hasDropdown" />
              </button>
            </div>
          </div>
        </div>
      </nav>

      <!-- Mobile Navigation Toggle -->
      <div class="mobile-nav-header">
        <div class="mobile-actions">
          <button class="language-btn mobile">
            <span class="language-icon">🌐</span>
            English
            <ChevronDown :size="14" />
          </button>
          <button class="search-btn mobile" aria-label="Search">
            <Search :size="18" />
          </button>
        </div>
        <button
          class="mobile-menu-btn"
          @click="toggleMobileMenu"
          :aria-label="isMobileMenuOpen ? 'Close menu' : 'Open menu'"
        >
          <Menu :size="24" v-if="!isMobileMenuOpen" />
          <span v-if="!isMobileMenuOpen" class="menu-text">MAIN MENU</span>
          <X :size="24" v-if="isMobileMenuOpen" />
          <span v-if="isMobileMenuOpen" class="menu-text">CLOSE MENU</span>
        </button>
      </div>
    </div>

    <!-- Mobile Menu -->
    <transition name="slide">
      <div v-if="isMobileMenuOpen" class="mobile-menu">
        <div class="mobile-menu-content">
          <!-- Main Nav Items -->
          <div class="mobile-main-nav">
            <div
              v-for="(item, index) in mainNavItems"
              :key="item.text"
              class="mobile-nav-item"
            >
              <button
                class="mobile-nav-link"
                @click="toggleDropdown(index)"
              >
                {{ item.text }}
                <Plus
                  :size="20"
                  class="plus-icon"
                  :class="{ 'rotated': activeDropdown === index }"
                />
              </button>
              <transition name="expand">
                <div v-if="activeDropdown === index" class="mobile-dropdown">
                  <a
                    v-for="subItem in item.items"
                    :key="subItem"
                    href="#"
                    class="mobile-dropdown-link"
                  >
                    {{ subItem }}
                  </a>
                </div>
              </transition>
            </div>
          </div>

          <!-- Secondary Nav Items -->
          <div class="mobile-secondary-nav">
            <a
              v-for="item in topNavItems"
              :key="item.text"
              :href="item.url"
              class="mobile-secondary-link"
              @click="closeMobileMenu"
            >
              {{ item.text }}
            </a>
          </div>
        </div>
      </div>
    </transition>
  </header>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  transition: all 0.3s ease;
  background-color: transparent;
}

.navbar.scrolled {
  background-color: white;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.navbar-container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

/* Logo */
.logo-link {
  display: flex;
  align-items: center;
  padding: 15px 0;
}

.logo {
  height: 60px;
  width: auto;
  filter: brightness(0) invert(1);
  transition: filter 0.3s ease;
}

.logo.logo-scrolled {
  filter: none;
}

/* Desktop Navigation */
.desktop-nav {
  display: flex;
  flex-direction: column;
  flex: 1;
  margin-left: 40px;
}

.top-nav {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  padding: 10px 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
}

.navbar.scrolled .top-nav {
  border-bottom-color: #e0e0e0;
}

.top-nav-links {
  display: flex;
  gap: 20px;
}

.top-nav-link {
  color: white;
  font-size: 13px;
  text-decoration: none;
  transition: color 0.3s;
  font-weight: 500;
  padding: 5px 0;
}

.navbar.scrolled .top-nav-link {
  color: #333;
}

.top-nav-link:hover {
  color: #ffb500;
}

.top-nav-actions {
  display: flex;
  align-items: center;
}

.language-btn {
  display: flex;
  align-items: center;
  gap: 6px;
  background: none;
  border: none;
  color: white;
  font-size: 13px;
  cursor: pointer;
  padding: 5px 10px;
  transition: color 0.3s;
}

.navbar.scrolled .language-btn {
  color: #333;
}

.language-btn:hover {
  color: #ffb500;
}

.language-icon {
  font-size: 16px;
}

/* Main Navigation */
.main-nav {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  gap: 30px;
  padding: 15px 0;
}

.search-btn {
  background: none;
  border: none;
  color: white;
  cursor: pointer;
  display: flex;
  align-items: center;
  padding: 8px;
  transition: color 0.3s;
}

.navbar.scrolled .search-btn {
  color: #333;
}

.search-btn:hover {
  color: #ffb500;
}

.main-nav-links {
  display: flex;
  justify-content: flex-end;
  gap: 30px;
}

.nav-item {
  position: relative;
}

.nav-link {
  display: flex;
  align-items: center;
  gap: 6px;
  background: none;
  border: none;
  color: white;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  padding: 8px 0;
  transition: color 0.3s;
  font-family: 'Open Sans', sans-serif;
}

.navbar.scrolled .nav-link {
  color: #333;
}

.nav-link:hover {
  color: #ffb500;
}

/* Mobile Navigation */
.mobile-nav-header {
  display: none;
}

.mobile-menu {
  display: none;
}

/* Responsive */
@media (max-width: 1024px) {
  .desktop-nav {
    display: none;
  }

  .mobile-nav-header {
    display: flex;
    align-items: center;
    gap: 15px;
  }

  .mobile-actions {
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .language-btn.mobile,
  .search-btn.mobile {
    color: white;
    font-size: 12px;
    padding: 6px 10px;
  }

  .navbar.scrolled .language-btn.mobile,
  .navbar.scrolled .search-btn.mobile {
    color: #333;
  }

  .mobile-menu-btn {
    display: flex;
    align-items: center;
    gap: 8px;
    background-color: #00566B;
    color: white;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    font-weight: 600;
    font-size: 13px;
    border-radius: 4px;
    transition: background-color 0.3s;
  }

  .mobile-menu-btn:hover {
    background-color: #004455;
  }

  .menu-text {
    font-family: 'Open Sans', sans-serif;
  }

  .mobile-menu {
    display: block;
    position: fixed;
    top: 90px;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: white;
    overflow-y: auto;
    -webkit-overflow-scrolling: touch;
  }

  .mobile-menu-content {
    padding: 20px;
  }

  .mobile-main-nav {
    background-color: #00566B;
    border-radius: 8px;
    overflow: hidden;
    margin-bottom: 20px;
  }

  .mobile-nav-item {
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }

  .mobile-nav-item:last-child {
    border-bottom: none;
  }

  .mobile-nav-link {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: none;
    border: none;
    color: white;
    font-size: 16px;
    font-weight: 600;
    padding: 18px 20px;
    text-align: left;
    cursor: pointer;
    font-family: 'Open Sans', sans-serif;
  }

  .plus-icon {
    transition: transform 0.3s ease;
  }

  .plus-icon.rotated {
    transform: rotate(45deg);
  }

  .mobile-dropdown {
    background-color: rgba(0, 0, 0, 0.1);
    padding: 10px 0;
  }

  .mobile-dropdown-link {
    display: block;
    color: white;
    padding: 12px 40px;
    text-decoration: none;
    font-size: 14px;
    transition: background-color 0.3s;
  }

  .mobile-dropdown-link:hover {
    background-color: rgba(255, 255, 255, 0.1);
  }

  .mobile-secondary-nav {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  .mobile-secondary-link {
    color: #666;
    font-size: 16px;
    font-weight: 500;
    padding: 15px 20px;
    text-decoration: none;
    transition: color 0.3s;
    border-bottom: 1px solid #e0e0e0;
  }

  .mobile-secondary-link:hover {
    color: #00566B;
  }
}

/* Transitions */
.slide-enter-active,
.slide-leave-active {
  transition: transform 0.3s ease;
}

.slide-enter-from {
  transform: translateX(-100%);
}

.slide-leave-to {
  transform: translateX(-100%);
}

.expand-enter-active,
.expand-leave-active {
  transition: max-height 0.3s ease, opacity 0.3s ease;
  overflow: hidden;
}

.expand-enter-from,
.expand-leave-to {
  max-height: 0;
  opacity: 0;
}

.expand-enter-to,
.expand-leave-from {
  max-height: 500px;
  opacity: 1;
}
</style>
