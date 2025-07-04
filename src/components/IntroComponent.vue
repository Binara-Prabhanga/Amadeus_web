<script setup>
// Intro component for movie library section
</script>

<template>
  <section id="library" class="intro">
    <div class="container">
      <div class="intro-content">
        <h2 class="intro-title">MOVIE LIBRARY</h2>
        <p class="intro-text">
          Discover our extensive collection of movies spanning every genre imaginable. 
          From classic masterpieces to the latest blockbusters, our carefully curated 
          library offers something for every movie enthusiast. Search through thousands 
          of titles and create your personalized watchlist for the ultimate cinema experience.
        </p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.intro {
  padding: 80px 0;
  background: var(--bg-dark);
  position: relative;
}

.intro::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    180deg,
    rgba(26, 26, 26, 0.8) 0%,
    rgba(10, 10, 10, 0.95) 50%,
    rgba(26, 26, 26, 0.8) 100%
  );
}

.intro-content {
  text-align: center;
  max-width: 800px;
  margin: 0 auto;
  position: relative;
  z-index: 1;
}

.intro-title {
  color: var(--primary-color);
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: bold;
  margin-bottom: 2rem;
  letter-spacing: 2px;
  text-transform: uppercase;
  position: relative;
}

.intro-title::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 100px;
  height: 3px;
  background: var(--primary-color);
  border-radius: 2px;
}

.intro-text {
  color: var(--text-color);
  font-size: clamp(1.1rem, 2.5vw, 1.3rem);
  line-height: 1.8;
  opacity: 0.9;
  margin: 0;
}

/* Animation on scroll */
.intro-content {
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 1s ease-out 0.2s forwards;
}

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .intro {
    padding: 60px 0;
  }
  
  .intro-title {
    margin-bottom: 1.5rem;
    letter-spacing: 1px;
  }
  
  .intro-title::after {
    width: 80px;
    height: 2px;
  }
  
  .intro-text {
    line-height: 1.7;
  }
}

@media (max-width: 480px) {
  .intro {
    padding: 40px 0;
  }
  
  .intro-content {
    padding: 0 1rem;
  }
  
  .intro-title {
    margin-bottom: 1rem;
  }
  
  .intro-title::after {
    width: 60px;
  }
}

/* Large screens */
@media (min-width: 1200px) {
  .intro {
    padding: 100px 0;
  }
  
  .intro-content {
    max-width: 900px;
  }
  
  .intro-title::after {
    width: 120px;
    height: 4px;
  }
}

/* High contrast mode support */
@media (prefers-contrast: high) {
  .intro-title {
    color: #fff;
  }
  
  .intro-text {
    color: #fff;
    opacity: 1;
  }
}

/* Reduced motion support */
@media (prefers-reduced-motion: reduce) {
  .intro-content {
    animation: none;
    opacity: 1;
    transform: none;
  }
}
</style>
