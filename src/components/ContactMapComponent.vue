<script setup>
import { ref } from 'vue'

const form = ref({
  firstName: '',
  lastName: '',
  email: '',
  telephone: '',
  message: ''
})

const errors = ref({})
const isSubmitting = ref(false)

// Validation rules
const validateForm = () => {
  const newErrors = {}

  // First Name validation
  if (!form.value.firstName.trim()) {
    newErrors.firstName = 'First name is required'
  }

  // Last Name validation
  if (!form.value.lastName.trim()) {
    newErrors.lastName = 'Last name is required'
  }

  // Email validation
  if (!form.value.email.trim()) {
    newErrors.email = 'Email is required'
  } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.value.email)) {
    newErrors.email = 'Please enter a valid email address'
  }

  // Message validation
  if (!form.value.message.trim()) {
    newErrors.message = 'Message is required'
  }

  errors.value = newErrors
  return Object.keys(newErrors).length === 0
}

// Handle form submission
const handleSubmit = async (e) => {
  e.preventDefault()
  
  if (!validateForm()) {
    return
  }

  isSubmitting.value = true

  try {
    // Simulate form submission delay
    await new Promise(resolve => setTimeout(resolve, 1000))
    
    // Show form data in alert (as requested)
    const formData = {
      'First Name': form.value.firstName,
      'Last Name': form.value.lastName,
      'Email': form.value.email,
      'Telephone': form.value.telephone || 'Not provided',
      'Message': form.value.message
    }

    const alertMessage = Object.entries(formData)
      .map(([key, value]) => `${key}: ${value}`)
      .join('\n')

    alert(`Form Submitted Successfully!\n\n${alertMessage}`)

    // Reset form
    form.value = {
      firstName: '',
      lastName: '',
      email: '',
      telephone: '',
      message: ''
    }
    errors.value = {}

  } catch (error) {
    alert('There was an error submitting the form. Please try again.')
  } finally {
    isSubmitting.value = false
  }
}

// Clear error when user starts typing
const clearError = (field) => {
  if (errors.value[field]) {
    delete errors.value[field]
  }
}
</script>

<template>
  <section id="contact" class="contact-section">
    <div class="container">
      <h2 class="section-title">How to reach us</h2>
      <p class="section-subtitle">Get in touch for the ultimate cinema experience</p>
      
      <div class="contact-content">
        <!-- Contact Form -->
        <div class="form-container">
          <form @submit="handleSubmit" class="contact-form" novalidate>
            <div class="form-row">
              <div class="form-group">
                <label for="firstName" class="form-label">
                  First Name *
                </label>
                <input
                  id="firstName"
                  v-model="form.firstName"
                  type="text"
                  class="form-input"
                  :class="{ error: errors.firstName }"
                  @input="clearError('firstName')"
                  required
                  aria-describedby="firstName-error"
                />
                <span 
                  v-if="errors.firstName" 
                  id="firstName-error"
                  class="error-text"
                  role="alert"
                >
                  {{ errors.firstName }}
                </span>
              </div>

              <div class="form-group">
                <label for="lastName" class="form-label">
                  Last Name *
                </label>
                <input
                  id="lastName"
                  v-model="form.lastName"
                  type="text"
                  class="form-input"
                  :class="{ error: errors.lastName }"
                  @input="clearError('lastName')"
                  required
                  aria-describedby="lastName-error"
                />
                <span 
                  v-if="errors.lastName" 
                  id="lastName-error"
                  class="error-text"
                  role="alert"
                >
                  {{ errors.lastName }}
                </span>
              </div>
            </div>

            <div class="form-row">
              <div class="form-group">
                <label for="email" class="form-label">
                  Email *
                </label>
                <input
                  id="email"
                  v-model="form.email"
                  type="email"
                  class="form-input"
                  :class="{ error: errors.email }"
                  @input="clearError('email')"
                  required
                  aria-describedby="email-error"
                />
                <span 
                  v-if="errors.email" 
                  id="email-error"
                  class="error-text"
                  role="alert"
                >
                  {{ errors.email }}
                </span>
              </div>

              <div class="form-group">
                <label for="telephone" class="form-label">
                  Telephone
                </label>
                <input
                  id="telephone"
                  v-model="form.telephone"
                  type="tel"
                  class="form-input"
                />
              </div>
            </div>

            <div class="form-group">
              <label for="message" class="form-label">
                Message *
              </label>
              <textarea
                id="message"
                v-model="form.message"
                class="form-input form-textarea"
                :class="{ error: errors.message }"
                @input="clearError('message')"
                required
                rows="5"
                aria-describedby="message-error"
              ></textarea>
              <span 
                v-if="errors.message" 
                id="message-error"
                class="error-text"
                role="alert"
              >
                {{ errors.message }}
              </span>
            </div>

            <button 
              type="submit" 
              class="btn submit-btn"
              :disabled="isSubmitting"
            >
              <span v-if="isSubmitting" class="loading-spinner"></span>
              <span v-else>Send Message</span>
            </button>
          </form>
        </div>

        <!-- Map Container -->
        <div class="map-container">
          <div class="map-placeholder">
            <iframe
              src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3036.644896315998!2d-3.6129436843169743!3d40.44695067936164!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0xd42289b4d0c5d9b%3A0x4a0a0a0a0a0a0a0a!2sAmadeus%20IT%20Group%2C%20Salvador%20de%20Madariaga%2C%201%2C%2028027%20Madrid%2C%20Spain!5e0!3m2!1sen!2ses!4v1641234567890"
              width="100%"
              height="100%"
              style="border:0;"
              allowfullscreen=""
              loading="lazy"
              referrerpolicy="no-referrer-when-downgrade"
              title="Amadeus IT Group - Salvador de Madariaga, 1, 28027 Madrid, Spain"
            ></iframe>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact-section {
  padding: 80px 0;
  background: linear-gradient(135deg, var(--bg-dark) 0%, #1a1a1a 100%);
}

.section-title {
  color: var(--primary-color);
  text-align: center;
  font-size: clamp(2.5rem, 5vw, 4rem);
  margin-bottom: 1rem;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.section-subtitle {
  color: var(--text-color);
  text-align: center;
  font-size: 1.2rem;
  margin-bottom: 4rem;
  opacity: 0.8;
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  max-width: 1200px;
  margin: 0 auto;
}

.form-container {
  background: var(--secondary-color);
  padding: 40px;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.contact-form {
  width: 100%;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
  margin-bottom: 20px;
}

.form-group {
  margin-bottom: 25px;
}

.form-label {
  display: block;
  color: var(--text-color);
  font-weight: 500;
  margin-bottom: 8px;
  font-size: 1rem;
}

.form-input {
  width: 100%;
  padding: 15px;
  border: 2px solid rgba(255, 255, 255, 0.1);
  background: rgba(255, 255, 255, 0.05);
  color: var(--text-color);
  border-radius: 6px;
  font-size: 1rem;
  transition: var(--transition);
}

.form-input:focus {
  border-color: var(--primary-color);
  background: rgba(255, 255, 255, 0.1);
  outline: none;
}

.form-input.error {
  border-color: var(--error-color);
  background: rgba(255, 68, 68, 0.1);
}

.form-textarea {
  resize: vertical;
  min-height: 120px;
}

.error-text {
  display: block;
  color: var(--error-color);
  font-size: 0.875rem;
  margin-top: 5px;
}

.submit-btn {
  width: 100%;
  padding: 15px;
  font-size: 1.1rem;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
  position: relative;
  min-height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.loading-spinner {
  width: 20px;
  height: 20px;
  border: 2px solid var(--secondary-color);
  border-top: 2px solid transparent;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

.map-container {
  display: flex;
  align-items: stretch;
}

.map-placeholder {
  width: 100%;
  background: var(--secondary-color);
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  min-height: 500px;
}

/* Responsive Design */
@media (max-width: 1024px) {
  .contact-content {
    gap: 40px;
  }
  
  .form-container,
  .map-placeholder {
    padding: 30px;
  }
}

@media (max-width: 768px) {
  .contact-section {
    padding: 60px 0;
  }
  
  .contact-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  
  .form-row {
    grid-template-columns: 1fr;
    gap: 0;
  }
  
  .form-container {
    padding: 25px;
  }
  
  .map-placeholder {
    min-height: 400px;
  }
  
  .map-content {
    padding: 30px;
  }
}

@media (max-width: 480px) {
  .section-subtitle {
    margin-bottom: 3rem;
  }
  
  .form-container {
    padding: 20px;
  }
  
  .map-content {
    padding: 20px;
  }
  
  .map-content h3 {
    font-size: 1.5rem;
  }
}

/* High contrast mode */
@media (prefers-contrast: high) {
  .form-input {
    border-color: var(--text-color);
  }
  
  .form-input:focus {
    border-color: var(--primary-color);
    border-width: 3px;
  }
}

/* Accessibility improvements */
.form-input:invalid:not(:placeholder-shown) {
  border-color: var(--error-color);
}

@media (prefers-reduced-motion: reduce) {
  .loading-spinner {
    animation: none;
  }
  
  .form-input,
  .submit-btn {
    transition: none;
  }
}
</style>
