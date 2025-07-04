<script setup>
import { ref, watch } from 'vue'
import batmanImg from '../assets/Images/Batman.jpg'
import wildWestImg from '../assets/Images/Wild West.jpg'
import spidermanImg from '../assets/Images/Spiderman.jpg'
import searchIcon from '../assets/Icons/Search White.svg'
import closeIcon from '../assets/Icons/Close White.svg'

const searchTerm = ref('')
const movies = ref([
  {
    id: 1,
    title: 'Batman Returns',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
    image: batmanImg,
    year: '1992',
    rating: '7.0'
  },
  {
    id: 2,
    title: 'Wild Wild West',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
    image: wildWestImg,
    year: '1999',
    rating: '4.9'
  },
  {
    id: 3,
    title: 'The Amazing Spiderman',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
    image: spidermanImg,
    year: '2012',
    rating: '6.9'
  }
])
const isLoading = ref(false)
const error = ref('')

// Search movies from TVMaze API
const searchMovies = async () => {
  if (!searchTerm.value.trim()) return

  isLoading.value = true
  error.value = ''

  try {
    const response = await fetch(`https://api.tvmaze.com/search/shows?q=${encodeURIComponent(searchTerm.value)}`)
    
    if (!response.ok) {
      throw new Error('Failed to fetch movies')
    }

    const data = await response.json()
    
    // Transform API data to our format
    const newMovies = data.map(item => ({
      id: item.show.id,
      title: item.show.name,
      description: item.show.summary ? 
        item.show.summary.replace(/<[^>]*>/g, '').substring(0, 150) + '...' : 
        'No description available',
      image: item.show.image?.medium || item.show.image?.original || '/placeholder-movie.jpg',
      year: item.show.premiered ? new Date(item.show.premiered).getFullYear() : 'Unknown',
      rating: item.show.rating?.average || 'N/A'
    }))

    // Add new movies without removing existing ones
    newMovies.forEach(newMovie => {
      if (!movies.value.some(movie => movie.id === newMovie.id)) {
        movies.value.push(newMovie)
      }
    })

    searchTerm.value = ''
  } catch (err) {
    error.value = 'Failed to fetch movies. Please try again.'
    console.error('Error fetching movies:', err)
  } finally {
    isLoading.value = false
  }
}

// Remove movie from grid
const removeMovie = (movieId) => {
  movies.value = movies.value.filter(movie => movie.id !== movieId)
}

// Handle form submission
const handleSubmit = (e) => {
  e.preventDefault()
  searchMovies()
}

// Handle enter key in search input
const handleKeyPress = (e) => {
  if (e.key === 'Enter') {
    searchMovies()
  }
}
</script>

<template>
  <section class="movie-grid-section">
    <div class="container">
      <!-- Search Section -->
      <div class="search-section">
        <h2>Collect your favourites</h2>
        <div class="search-container">
          <form @submit="handleSubmit" class="search-form">
            <div class="search-input-group">
              <input
                v-model="searchTerm"
                type="text"
                placeholder="Search title and add to grid"
                class="search-input"
                @keypress="handleKeyPress"
                :disabled="isLoading"
              />
              <button 
                type="submit" 
                class="search-btn"
                :disabled="isLoading || !searchTerm.trim()"
                aria-label="Search movies"
              >
                <img :src="searchIcon" alt="Search" class="search-icon" />
              </button>
            </div>
          </form>
        </div>
        
        <!-- Error message -->
        <div v-if="error" class="error-message" role="alert">
          {{ error }}
        </div>
      </div>

      <!-- Movies Grid -->
      <div class="movies-grid" v-if="movies.length > 0">
        <div 
          v-for="movie in movies" 
          :key="movie.id"
          class="movie-card"
        >
          <button 
            class="close-btn"
            @click="removeMovie(movie.id)"
            aria-label="Remove movie from grid"
          >
            <img :src="closeIcon" alt="Close" class="close-icon" />
          </button>
          
          <div class="movie-image">
            <img 
              :src="movie.image" 
              :alt="movie.title"
              @error="$event.target.src = '/placeholder-movie.jpg'"
            />
          </div>
          
          <div class="movie-info">
            <h3 class="movie-title">{{ movie.title }}</h3>
            <div class="movie-meta">
              <span class="movie-year">{{ movie.year }}</span>
              <span class="movie-rating" v-if="movie.rating !== 'N/A'">
                ⭐ {{ movie.rating }}
              </span>
            </div>
            <p class="movie-description">{{ movie.description }}</p>
          </div>
        </div>
      </div>

      <!-- Empty state -->
      <div v-else class="empty-state">
        <div class="empty-content">
          <div class="empty-icon">🎬</div>
          <h3>No movies added yet</h3>
          <p>Search for your favorite movies and add them to your collection</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.movie-grid-section {
  padding: 80px 0;
  background: var(--bg-dark);
  min-height: 600px;
}

.search-section {
  text-align: center;
  margin-bottom: 60px;
}

.search-section h2 {
  color: var(--text-color);
  font-size: clamp(2rem, 4vw, 3rem);
  margin-bottom: 2rem;
  font-weight: 300;
}

.search-container {
  max-width: 600px;
  margin: 0 auto;
}

.search-form {
  width: 100%;
}

.search-input-group {
  display: flex;
  background: transparent;
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 4px;
  padding: 2px;
  box-shadow: none;
}

.search-input {
  flex: 1;
  padding: 12px 16px;
  border: none;
  background: transparent;
  color: var(--text-color);
  font-size: 1rem;
  outline: none;
}

.search-input::placeholder {
  color: rgba(255, 255, 255, 0.5);
  font-size: 0.9rem;
}

.search-btn {
  background: transparent;
  border: none;
  padding: 12px 16px;
  cursor: pointer;
  transition: var(--transition);
  min-width: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.search-icon {
  width: 20px;
  height: 20px;
  opacity: 0.7;
}

.search-btn:hover:not(:disabled) .search-icon {
  opacity: 1;
}

.search-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
  transform: none;
}

.loading-spinner {
  width: 20px;
  height: 20px;
  border: 2px solid var(--secondary-color);
  border-top: 2px solid transparent;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.error-message {
  color: var(--error-color);
  margin-top: 1rem;
  padding: 10px;
  background: rgba(255, 68, 68, 0.1);
  border-radius: 4px;
  border: 1px solid var(--error-color);
}

.movies-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 30px;
  max-width: 1200px;
  margin: 0 auto;
}

.movie-card {
  background: var(--secondary-color);
  border-radius: 12px;
  overflow: hidden;
  transition: var(--transition);
  position: relative;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
}

.movie-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.4);
}

.close-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  background: rgba(0, 0, 0, 0.7);
  border: none;
  width: 30px;
  height: 30px;
  border-radius: 4px;
  cursor: pointer;
  z-index: 10;
  transition: var(--transition);
  display: flex;
  align-items: center;
  justify-content: center;
}

.close-icon {
  width: 12px;
  height: 12px;
}

.close-btn:hover {
  background: rgba(0, 0, 0, 0.9);
}

.movie-image {
  width: 100%;
  height: 400px;
  overflow: hidden;
  position: relative;
}

.movie-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: var(--transition);
}

.movie-card:hover .movie-image img {
  transform: scale(1.05);
}

.movie-info {
  padding: 20px;
}

.movie-title {
  color: var(--text-color);
  font-size: 1.3rem;
  margin-bottom: 10px;
  font-weight: bold;
  line-height: 1.3;
}

.movie-meta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 15px;
  font-size: 0.9rem;
}

.movie-year {
  color: var(--primary-color);
  font-weight: bold;
}

.movie-rating {
  color: var(--text-color);
  opacity: 0.8;
}

.movie-description {
  color: var(--text-color);
  opacity: 0.8;
  line-height: 1.6;
  font-size: 0.95rem;
}

.empty-state {
  text-align: center;
  padding: 80px 20px;
}

.empty-content {
  max-width: 400px;
  margin: 0 auto;
}

.empty-icon {
  font-size: 4rem;
  margin-bottom: 20px;
  opacity: 0.5;
}

.empty-state h3 {
  color: var(--text-color);
  margin-bottom: 15px;
  opacity: 0.7;
}

.empty-state p {
  color: var(--text-color);
  opacity: 0.5;
  line-height: 1.6;
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .movie-grid-section {
    padding: 60px 0;
  }
  
  .movies-grid {
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 20px;
  }
  
  .search-input-group {
    flex-direction: column;
    gap: 10px;
  }
  
  .search-btn {
    width: 100%;
  }
}

@media (max-width: 480px) {
  .movies-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }
  
  .movie-image {
    height: 300px;
  }
}

/* Large screens */
@media (min-width: 1200px) {
  .movies-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

/* High contrast mode */
@media (prefers-contrast: high) {
  .movie-card {
    border: 1px solid var(--text-color);
  }
  
  .search-input-group {
    border: 1px solid var(--text-color);
  }
}
</style>
