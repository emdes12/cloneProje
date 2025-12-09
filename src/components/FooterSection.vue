<script setup>
import { Facebook, Youtube, Instagram } from 'lucide-vue-next'

const links = [
  { text: 'Policies and Regulations', url: '#' },
  { text: 'Freedom of Information Act', url: '#' },
  { text: 'Nondiscrimination', url: '#' },
  { text: 'Web Accessibility Guidelines', url: '#' },
  { text: 'Website Feedback', url: '#' },
  { text: 'Safety Tipline', url: '#' },
  { text: 'Contact Us', url: '#' },
]

const socialMedia = [
  { name: 'Facebook', icon: 'facebook', url: '#', color: '#3b5998' },
  { name: 'X (Twitter)', icon: 'x', url: '#', color: '#000000' },
  { name: 'YouTube', icon: 'youtube', url: '#', color: '#FF0000' },
  {
    name: 'Instagram',
    icon: 'instagram',
    url: '#',
    color: 'linear-gradient(45deg, #f09433 0%,#e6683c 25%,#dc2743 50%,#cc2366 75%,#bc1888 100%)',
  },
]
</script>
<template>
  <div class="sections">
    <div class="container">
      <a href="#">Schooogy</a>
      <a href="#">SIS</a>
      <a href="#">Google Workspace</a>
      <a href="#Librry">Library</a>
      <a href="#">School Meals</a>
      <a href="#">MySchoolBucks</a>
      <a href="#">Bus</a><a href="#Employee">Employee Resources</a>
    </div>
  </div>

  <footer>
    <!-- <img src="/download.svg" alt="footer background image" class="bottom-img" /> -->
    <div class="footer-section">
      <div class="footer-content">
        <!-- Top Section -->
        <div class="footer-top">
          <div class="footer-info">
            <h3 class="footer-title">Gatehouse Administration Center</h3>
            <p class="footer-address">8115 Gatehouse Road</p>
            <p class="footer-address">Falls Church, VA 22042</p>
            <a href="#" class="footer-link">Family Information Phone Lines</a>

            <div class="logo-container">
              <img
                src="/ed73bfec3313cda4977a67ffc9a621843d1e5858.png"
                alt="Educate Fairfax"
                class="footer-logo"
              />
            </div>
          </div>

          <div class="footer-links">
            <a v-for="link in links" :key="link.text" :href="link.url" class="footer-nav-link">
              {{ link.text }}
            </a>
          </div>
        </div>

        <!-- Social Media Section -->
        <div class="social-section">
          <h3 class="social-title">Follow FCPS on Social Media</h3>
          <div class="social-icons">
            <a href="#" class="social-icon facebook" aria-label="Facebook">
              <Facebook :size="20" />
            </a>
            <a href="#" class="social-icon twitter" aria-label="X (Twitter)">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                <path
                  d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"
                />
              </svg>
            </a>
            <a href="#" class="social-icon youtube" aria-label="YouTube">
              <Youtube :size="20" />
            </a>
            <a href="#" class="social-icon instagram" aria-label="Instagram">
              <Instagram :size="20" />
            </a>
          </div>
        </div>

        <!-- Spanish Social Media -->
        <div class="social-section">
          <h3 class="social-title">Social Media in Español (Spanish)</h3>
          <div class="social-icons">
            <a href="#" class="social-icon facebook" aria-label="Facebook Spanish">
              <Facebook :size="20" />
            </a>
            <a href="#" class="social-icon twitter" aria-label="X Spanish">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                <path
                  d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"
                />
              </svg>
            </a>
            <a href="#" class="social-icon youtube" aria-label="YouTube Spanish">
              <Youtube :size="20" />
            </a>
          </div>
        </div>

        <!-- Korean Social Media -->
        <div class="social-section">
          <h3 class="social-title">Social Media in 한국어 (Korean)</h3>
          <div class="social-icons">
            <a href="#" class="social-icon facebook" aria-label="Facebook Korean">
              <Facebook :size="20" />
            </a>
          </div>
        </div>
      </div>

      <!-- Copyright -->
      <div class="footer-copyright">
        <p>©Copyright 2025 Fairfax County School Board. All Rights Reserved.</p>
      </div>
    </div>
  </footer>
</template>
<style scoped>
.sections {
  background-color: #00566b;
  padding: 20px;
  font-family: 'Open Sans';
}

.sections .container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 30px;
}

a {
  color: #fff;
  font-size: 16px;
  font-weight: 600;
}

a:hover {
  color: #ffb500;
}

footer {
  background-color: #ededed;
  position: relative;
}

.footer-section {
  overflow: hidden;
  z-index: 1000;
  background-image: url(./download.svg);
  background-position: bottom center;
  background-size: contain;
  background-repeat: no-repeat;
}

.bottom-img {
  width: 100%;
  position: absolute;
  bottom: 0;
  left: 0;
  z-index: 1;
  right: 0;
  object-fit: cover;
  object-position: center;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
  z-index: 1;
  padding: 60px 20px 40px;
}

/* Top Section */
.footer-top {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  margin-bottom: 50px;
  padding-bottom: 40px;
  border-bottom: 1px solid #ddd;
}

.footer-info {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.footer-title {
  color: #00566b;
  font-size: 18px;
  font-weight: 700;
  margin: 0 0 5px 0;
  font-family: 'Open Sans', sans-serif;
}

.footer-address {
  color: #00566b;
  font-size: 14px;
  margin: 0;
  font-family: 'Open Sans', sans-serif;
}

.footer-link {
  color: #00566b;
  font-size: 14px;
  text-decoration: underline;
  margin-top: 10px;
  font-family: 'Open Sans', sans-serif;
  transition: color 0.3s;
}

.footer-link:hover {
  color: #ffb500;
}

.logo-container {
  margin-top: 25px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}

.footer-logo {
  width: 80px;
  height: auto;
}

.logo-text {
  color: #00566b;
  font-size: 14px;
  font-weight: 600;
  margin: 0;
  font-family: 'Open Sans', sans-serif;
}

.footer-links {
  display: flex;
  flex-direction: column;
  gap: 12px;
  padding-left: 40px;
  border-left: 1px solid #ddd;
}

.footer-nav-link {
  color: #333;
  font-size: 14px;
  text-decoration: none;
  font-family: 'Open Sans', sans-serif;
  transition: color 0.3s;
}

.footer-nav-link:hover {
  color: #00566b;
}

/* Social Media Sections */
.social-section {
  text-align: center;
  margin-bottom: 35px;
}

.social-title {
  color: #000;
  font-size: 16px;
  font-weight: 700;
  margin: 0 0 15px 0;
  font-family: 'Open Sans', sans-serif;
}

.social-icons {
  display: flex;
  justify-content: center;
  gap: 15px;
}

.social-icon {
  width: 48px;
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  text-decoration: none;
  transition:
    transform 0.3s,
    opacity 0.3s;
  border-radius: 4px;
}

.social-icon:hover {
  transform: translateY(-3px);
  opacity: 0.9;
}

.social-icon.facebook {
  background-color: #3b5998;
}

.social-icon.twitter {
  background-color: #000000;
}

.social-icon.youtube {
  background-color: #ff0000;
}

.social-icon.instagram {
  background: linear-gradient(
    45deg,
    #f09433 0%,
    #e6683c 25%,
    #dc2743 50%,
    #cc2366 75%,
    #bc1888 100%
  );
}

/* Wave Background */
.wave-container {
  position: relative;
  width: 100%;
  height: 120px;
  margin-top: 40px;
}

.wave {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

/* Copyright */
.footer-copyright {
  background-color: transparent;
  text-align: center;
  padding: 20px;
  position: relative;
  z-index: 1;
}

.footer-copyright p {
  color: #333;
  font-size: 12px;
  margin: 0;
  font-family: 'Open Sans', sans-serif;
}

/* Responsive */
@media (max-width: 768px) {
  .footer-content {
    padding: 40px 20px 30px;
  }

  .footer-top {
    grid-template-columns: 1fr;
    gap: 30px;
  }

  .footer-links {
    padding-left: 0;
    border-left: none;
    border-top: 1px solid #ddd;
    padding-top: 30px;
  }

  .footer-info {
    text-align: center;
  }

  .logo-container {
    align-items: center;
  }

  .social-icons {
    flex-wrap: wrap;
  }

  .social-icon {
    width: 44px;
    height: 44px;
  }

  .wave-container {
    height: 80px;
  }
}

@media (max-width: 480px) {
  .footer-title {
    font-size: 16px;
  }

  .footer-address,
  .footer-link,
  .footer-nav-link {
    font-size: 13px;
  }

  .social-title {
    font-size: 14px;
  }

  .social-icon {
    width: 40px;
    height: 40px;
  }
}
</style>
