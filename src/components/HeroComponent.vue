<script setup>
// Import assets properly for Vite
import headerVideo from '../assets/Videos/Header Video.mp4'
import headerImage from '../assets/Images/Header Image.jpg'
</script>

<template>
  <section id="home" class="hero">
    <div class="hero-content">
      <div class="hero-video">
        <!-- Hero Video -->
        <video 
          class="hero-video-element" 
          autoplay 
          muted 
          loop 
          playsinline
          :poster="headerImage"
        >
          <source :src="headerVideo" type="video/mp4">
          <!-- Fallback image if video doesn't load -->
          <img :src="headerImage" alt="Cinema theater with red seats" class="hero-fallback-img" />
        </video>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  position: relative;
  width: 100%;
  height: 100vh;
  min-height: 600px;
  margin-top: 80px; /* Account for fixed header */
  overflow: hidden;
}

.hero-content {
  position: relative;
  width: 100%;
  height: 100%;
}

.hero-video {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
}

.hero-video-element {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
}

.hero-fallback-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
}

.hero-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.4);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2;
}

.hero-text {
  text-align: center;
  max-width: 600px;
  padding: 2rem;
}

.hero-text h1 {
  color: var(--text-color);
  margin-bottom: 1rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
}

.hero-text p {
  color: var(--text-color);
  margin-bottom: 2rem;
  font-size: 1.2rem;
  opacity: 0.9;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.7);
}

.cta-button {
  font-size: 1.1rem;
  padding: 15px 30px;
  box-shadow: 0 4px 15px rgba(212, 175, 55, 0.3);
}

.cta-button:hover {
  box-shadow: 0 6px 20px rgba(212, 175, 55, 0.4);
}

@keyframes shimmer {
  0%, 100% {
    opacity: 0.3;
  }
  50% {
    opacity: 0.6;
  }
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .hero {
    height: 70vh;
    min-height: 500px;
    margin-top: 70px;
  }
  
  .hero-text {
    padding: 1rem;
  }
  
  .hero-text h1 {
    font-size: 2.5rem;
  }
  
  .hero-text p {
    font-size: 1.1rem;
  }
  
  .cta-button {
    padding: 12px 24px;
    font-size: 1rem;
  }
}

@media (max-width: 480px) {
  .hero {
    height: 60vh;
    min-height: 400px;
  }
  
  .hero-text h1 {
    font-size: 2rem;
  }
  
  .placeholder-content h2 {
    font-size: 1.5rem;
  }
  
  .placeholder-content p {
    font-size: 1rem;
  }
}

/* Large screens */
@media (min-width: 1200px) {
  .hero {
    margin-top: 90px;
  }
  
  .hero-text h1 {
    font-size: 4rem;
  }
  
  .hero-text p {
    font-size: 1.3rem;
  }
}
</style>
