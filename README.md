# 🎬 Amadeus Cinema Website

A responsive movie-themed website built with Vue.js 3 and Vite. Features a modern design with mobile-first responsive layout that adapts to Desktop, Tablet, and Mobile devices.

## 🚀 Features

- **Responsive Design**: Mobile-first approach with breakpoints for tablet and desktop
- **Vue 3 Composition API**: Modern Vue.js architecture with reactive components
- **Movie Search**: Integration with TVMaze API for dynamic movie data
- **Interactive Components**: Header with hamburger menu, movie grid, contact form
- **Accessibility**: WCAG compliant with proper ARIA labels and keyboard navigation
- **Modern Styling**: Pure CSS with custom properties and smooth transitions

## 🛠️ Tech Stack

- **Frontend**: Vue.js 3 with Composition API
- **Build Tool**: Vite
- **Language**: Vanilla JavaScript (ES6+)
- **Styling**: Pure CSS with CSS Grid and Flexbox
- **API**: TVMaze API for movie data

## 📁 Project Structure

```
src/
├── components/
│   ├── HeaderComponent.vue      # Navigation with responsive menu
│   ├── HeroComponent.vue        # Hero section with placeholder for image/video
│   ├── IntroComponent.vue       # Movie library introduction
│   ├── MovieGridComponent.vue   # Movie search and grid display
│   ├── ContactMapComponent.vue  # Contact form and map placeholder
│   └── FooterComponent.vue      # Footer with company info and social links
├── App.vue                      # Main application component
├── main.js                      # Application entry point
└── style.css                    # Global styles
```

## 🎯 Components Overview

### HeaderComponent
- Logo and navigation menu
- Responsive hamburger menu for mobile
- Smooth transitions and hover effects
- Accessibility features with ARIA labels

### HeroComponent
- Full-width hero section with placeholder for image/video
- Responsive text and call-to-action button
- Overlay content with gradient background

### IntroComponent
- Movie library introduction section
- Centered content with animated appearance
- Responsive typography

### MovieGridComponent
- Search functionality with TVMaze API integration
- Dynamic movie grid (3 columns on desktop, responsive on mobile)
- Movie cards with poster, title, description, and close button
- Loading states and error handling

### ContactMapComponent
- Contact form with validation
- Required fields: First Name, Last Name, Email, Message
- Optional telephone field
- Google Maps placeholder section
- Form submission with alert display

### FooterComponent
- Company information: "Amadeus Hotels"
- Dynamic copyright year
- Social media links (placeholders)
- Newsletter signup
- Legal links

## 🎨 Design Features

- **Color Scheme**: Dark theme with gold accents (#d4af37)
- **Typography**: Responsive font sizes using clamp()
- **Animations**: Smooth transitions and hover effects
- **Grid System**: CSS Grid for layouts, Flexbox for components
- **Mobile-First**: Responsive design starting from mobile breakpoints

## 🚀 Getting Started

1. **Install Dependencies**:
   ```bash
   npm install
   ```

2. **Development Server**:
   ```bash
   npm run dev
   ```

3. **Build for Production**:
   ```bash
   npm run build
   ```

4. **Preview Production Build**:
   ```bash
   npm run preview
   ```

## 📱 Responsive Breakpoints

- **Mobile**: < 768px (single column layout)
- **Tablet**: 768px - 1024px (2 column layout)
- **Desktop**: > 1024px (3 column layout)

## 🔌 API Integration

The website integrates with the TVMaze API for movie data:
- **Endpoint**: `https://api.tvmaze.com/search/shows?q=searchTerm`
- **Features**: Search movies, add to grid, remove from grid
- **Error Handling**: Loading states and error messages

## 🎯 Future Enhancements

- Add actual movie poster images
- Implement Google Maps integration
- Add movie detail modal
- Include video background for hero section
- Add more advanced filtering options
- Implement user favorites functionality

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🏢 About Amadeus Hotels

Amadeus Hotels - Premium cinema experience with cutting-edge technology and comfortable seating for the ultimate movie-watching experience.
