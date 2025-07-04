<script setup>
import HeaderComponent from './components/HeaderComponent.vue'
import HeroComponent from './components/HeroComponent.vue'
import IntroComponent from './components/IntroComponent.vue'
import MovieGridComponent from './components/MovieGridComponent.vue'
import ContactMapComponent from './components/ContactMapComponent.vue'
import FooterComponent from './components/FooterComponent.vue'
</script>

<template>
  <div id="app">
    <HeaderComponent />
    <main>
      <HeroComponent />
      <IntroComponent />
      <MovieGridComponent />
      <ContactMapComponent />
    </main>
    <FooterComponent />
  </div>
</template>

<style>
:root {
  --primary-color: #d4af37;
  --secondary-color: #1a1a1a;
  --text-color: #ffffff;
  --text-dark: #333333;
  --bg-dark: #0a0a0a;
  --bg-light: #f5f5f5;
  --error-color: #ff4444;
  --success-color: #44ff44;
  --transition: all 0.3s ease;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Arial', sans-serif;
  line-height: 1.6;
  color: var(--text-color);
  background-color: var(--bg-dark);
}

#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  width: 100%;
  margin: 0;
  padding: 0;
}

main {
  flex: 1;
}

/* Accessibility */
button:focus,
input:focus,
textarea:focus {
  outline: 2px solid var(--primary-color);
  outline-offset: 2px;
}

/* Smooth scrolling */
html {
  scroll-behavior: smooth;
}

/* RTL Support */
[dir="rtl"] .nav-links {
  flex-direction: row-reverse;
}

[dir="rtl"] .contact-content {
  direction: rtl;
}

[dir="rtl"] .footer-content {
  direction: rtl;
}

[dir="rtl"] .movies-grid {
  direction: rtl;
}

[dir="rtl"] .form-row {
  direction: rtl;
}

[dir="rtl"] .social-icons {
  flex-direction: row-reverse;
}

/* Common utility classes */
.container {
  max-width:inherit;
  margin: 0 0;
  padding: 0 20px;
}

.btn {
  background: var(--primary-color);
  color: var(--secondary-color);
  border: none;
  padding: 12px 24px;
  cursor: pointer;
  border-radius: 4px;
  font-weight: bold;
  text-transform: uppercase;
  transition: var(--transition);
}

.btn:hover {
  background: #c19b26;
  transform: translateY(-2px);
}

.btn:active {
  transform: translateY(0);
}

/* Responsive text sizes */
h1 {
  font-size: clamp(2rem, 5vw, 3.5rem);
}

h2 {
  font-size: clamp(1.5rem, 4vw, 2.5rem);
}

h3 {
  font-size: clamp(1.25rem, 3vw, 2rem);
}

p {
  font-size: clamp(1rem, 2.5vw, 1.125rem);
}
</style>
