<script setup>
import { ref, onMounted } from 'vue'
import twitterIcon from '../assets/Icons/Twitter White.svg'
import youtubeIcon from '../assets/Icons/Youtube White.svg'

const currentYear = ref(new Date().getFullYear())

onMounted(() => {
  // Update year dynamically
  currentYear.value = new Date().getFullYear()
})
</script>

<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <!-- Company Info -->
        <div class="footer-section company-info">
          <h3 class="company-name">Amadeus IT Group</h3>
          <div class="address">
            <p>© Salvador de Madariaga, 1</p>
            <p>28027 Madrid</p>
            <p>Spain</p>
          </div>
        </div>

        <!-- Social Media -->
        <div class="footer-section social-section">
          <div class="social-icons">
            <a href="#" class="social-link" aria-label="Follow us on Twitter">
              <span class="social-text">Follow us on</span>
              <img :src="twitterIcon" alt="Twitter" class="social-icon" />
            </a>
            <a href="#" class="social-link" aria-label="Subscribe to our YouTube channel">
              <img :src="youtubeIcon" alt="YouTube" class="social-icon" />
            </a>
          </div>
        </div>
      </div>

      <!-- Copyright Bar -->
      <div class="copyright-bar">
        <div class="copyright-content">
          <p class="copyright-text">
            © {{ currentYear }} Amadeus IT Group. All rights reserved.
          </p>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: linear-gradient(180deg, var(--secondary-color) 0%, #0a0a0a 100%);
  color: var(--text-color);
  margin-top: auto;
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding: 40px 0 30px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.company-info {
  flex: 1;
}

.company-name {
  font-size: 1.2rem;
  font-weight: normal;
  margin-bottom: 15px;
  color: var(--text-color);
}

.address p {
  margin-bottom: 4px;
  opacity: 0.8;
  line-height: 1.5;
  font-size: 0.9rem;
}

.social-section {
  display: flex;
  align-items: center;
}

.social-icons {
  display: flex;
  align-items: center;
  gap: 20px;
}

.social-link {
  display: flex;
  align-items: center;
  gap: 8px;
  color: var(--text-color);
  text-decoration: none;
  transition: var(--transition);
}

.social-text {
  font-size: 0.9rem;
  opacity: 0.8;
}

.social-icon {
  width: 20px;
  height: 20px;
  opacity: 0.8;
  transition: var(--transition);
}

.social-link:hover .social-icon {
  opacity: 1;
}

.copyright-bar {
  padding: 25px 0;
}

.copyright-content {
  display: flex;
  justify-content: center;
  align-items: center;
}

.copyright-text {
  margin: 0;
  opacity: 0.7;
  font-size: 0.9rem;
  text-align: center;
}

/* Responsive Design */
@media (max-width: 768px) {
  .footer-content {
    flex-direction: column;
    gap: 30px;
    padding: 30px 0 20px;
    text-align: center;
  }
  
  .social-icons {
    justify-content: center;
  }
  
  .copyright-content {
    padding: 15px 0;
  }
}

@media (max-width: 480px) {
  .company-name {
    font-size: 1.5rem;
  }
  
  .social-icons {
    gap: 15px;
  }
}

/* High contrast mode */
@media (prefers-contrast: high) {
  .footer {
    background: #000;
  }
  
  .footer-section h3,
  .footer-section h4,
  .footer-section h5 {
    color: #fff;
  }
  
  .social-icon {
    border: 1px solid var(--text-color);
  }
}

/* Reduced motion */
@media (prefers-reduced-motion: reduce) {
  .social-icon,
  .quick-links a,
  .newsletter-btn {
    transition: none;
  }
  
  .social-icon:hover {
    transform: none;
  }
}
</style>
