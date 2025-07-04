<script setup>
import { ref } from 'vue'
import logoWhite from '../assets/Logos/Logo White.svg'

const isMenuOpen = ref(false)

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}
</script>

<template>
  <header class="header">
    <div class="container">
      <nav class="navbar">
        <!-- Logo -->
        <div class="logo">
          <img :src="logoWhite" alt="Logoipsum" class="logo-img" />
        </div>

        <!-- Desktop Navigation -->
        <ul class="nav-links desktop-nav">
          <li><a href="#home" @click="closeMenu">HOME</a></li>
          <li><a href="#screens" @click="closeMenu">OUR SCREENS</a></li>
          <li><a href="#schedule" @click="closeMenu">SCHEDULE</a></li>
          <li><a href="#library" @click="closeMenu">MOVIE LIBRARY</a></li>
          <li><a href="#contact" @click="closeMenu">LOCATION & CONTACT</a></li>
        </ul>

        <!-- Hamburger Menu -->
        <div 
          class="hamburger" 
          :class="{ active: isMenuOpen }"
          @click="toggleMenu"
          role="button"
          tabindex="0"
          aria-label="Toggle navigation menu"
          @keydown.enter="toggleMenu"
          @keydown.space="toggleMenu"
        >
          <span></span>
          <span></span>
          <span></span>
        </div>

        <!-- Mobile Navigation -->
        <ul class="nav-links mobile-nav" :class="{ active: isMenuOpen }">
          <li><a href="#home" @click="closeMenu">HOME</a></li>
          <li><a href="#screens" @click="closeMenu">OUR SCREENS</a></li>
          <li><a href="#schedule" @click="closeMenu">SCHEDULE</a></li>
          <li><a href="#library" @click="closeMenu">MOVIE LIBRARY</a></li>
          <li><a href="#contact" @click="closeMenu">LOCATION & CONTACT</a></li>
        </ul>
      </nav>
    </div>
  </header>
</template>

<style scoped>
.header {
  background: var(--secondary-color);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  min-height: 80px;
}

.logo {
  display: flex;
  align-items: left;
  margin-right: auto;
}

.logo-img {
  height: 40px;
  width: auto;
  align-items: left;
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 2rem;
  margin-left: auto;
}

.nav-links a {
  color: var(--text-color);
  text-decoration: none;
  font-weight: 500;
  font-size: 0.9rem;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  transition: var(--transition);
  position: relative;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.nav-links a:hover {
  color: var(--primary-color);
  background: rgba(212, 175, 55, 0.1);
}

.nav-links a::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  width: 0;
  height: 2px;
  background: var(--primary-color);
  transition: var(--transition);
  transform: translateX(-50%);
}

.nav-links a:hover::after {
  width: 80%;
}

.hamburger {
  display: none;
  flex-direction: column;
  cursor: pointer;
  padding: 0.5rem;
  border-radius: 4px;
  transition: var(--transition);
  margin-left: auto;
}

.hamburger:hover {
  background: rgba(212, 175, 55, 0.1);
}

.hamburger span {
  width: 25px;
  height: 3px;
  background: var(--text-color);
  margin: 3px 0;
  transition: var(--transition);
  border-radius: 2px;
}

.hamburger.active span:nth-child(1) {
  transform: rotate(-45deg) translate(-5px, 6px);
}

.hamburger.active span:nth-child(2) {
  opacity: 0;
}

.hamburger.active span:nth-child(3) {
  transform: rotate(45deg) translate(-5px, -6px);
}

.mobile-nav {
  display: none;
}

/* Tablet and Mobile Styles */
@media (max-width: 768px) {
  .desktop-nav {
    display: none;
  }

  .hamburger {
    display: flex;
  }

  .mobile-nav {
    display: flex;
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background: var(--secondary-color);
    flex-direction: column;
    gap: 0;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.3s ease;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
  }

  .mobile-nav.active {
    max-height: 300px;
  }

  .mobile-nav li {
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }

  .mobile-nav li:last-child {
    border-bottom: none;
  }

  .mobile-nav a {
    display: block;
    padding: 1rem 2rem;
    border-radius: 0;
  }

  .mobile-nav a::after {
    display: none;
  }
}

/* Large screens */
@media (min-width: 1200px) {
  .nav-links {
    gap: 3rem;
  }
  
  .nav-links a {
    padding: 0.75rem 1.5rem;
  }
}
</style>
