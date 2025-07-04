# Copilot Instructions for Amadeus Cinema Website

<!-- Use this file to provide workspace-specific custom instructions to Copilot. For more details, visit https://code.visualstudio.com/docs/copilot/copilot-customization#_use-a-githubcopilotinstructionsmd-file -->

## Project Overview
This is a Vue.js movie cinema website with responsive design for Desktop, Tablet, and Mobile views.

## Tech Stack
- **Frontend**: Vue.js 3 with Composition API
- **Styling**: Pure CSS (no Bootstrap/Tailwind)
- **Build Tool**: Vite
- **Language**: Vanilla JavaScript (no TypeScript/jQuery)
- **API**: TVMaze API for movie data

## Component Structure
- `HeaderComponent`: Navigation with hamburger menu for mobile
- `HeroComponent`: Hero section with responsive image
- `IntroComponent`: Movie library introduction text
- `MovieGridComponent`: Movie search and grid display
- `ContactMapComponent`: Contact form and Google Maps
- `FooterComponent`: Company info and social links

## Design Requirements
- Mobile-first responsive design
- Pure CSS with media queries
- Hover effects and smooth transitions
- Form validation with error handling
- Dynamic year in footer
- WCAG accessibility compliance

## API Integration
- Fetch movie data from: `https://api.tvmaze.com/search/shows?q=searchTerm`
- Add movies dynamically to grid without removing existing ones
- Each movie card should have close button to remove from grid

## Code Style
- Use Vue 3 Composition API
- Component-based architecture
- Semantic HTML5 elements
- CSS custom properties for theming
- Clean, readable JavaScript
