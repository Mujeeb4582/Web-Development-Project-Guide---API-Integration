# Recipe Website Project - Complete Setup Guide 🍳

## 1. Project Setup

### Create Project Structure
```
recipe-website/
├── css/
│   └── style.css
├── js/
│   ├── api.js
│   └── script.js
└── index.html
```

### API Information
We'll use TheMealDB API (Free, no authentication required)
Base URL: `https://www.themealdb.com/api/json/v1/1`

Available Endpoints:
```javascript
Search meals by name: /search.php?s={query}
Get meal by ID: /lookup.php?i={id}
Random meal: /random.php
List categories: /categories.php
Filter by category: /filter.php?c={category}
```

## 2. Initial Files Setup

### index.html - Basic Structure
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Recipe Finder</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <!-- Header -->
    <header>
        <nav>
            <h1>Recipe Finder</h1>
            <div class="search-container">
                <input type="text" id="searchInput" placeholder="Search recipes...">
                <button id="searchBtn">Search</button>
            </div>
            <button id="randomRecipeBtn">Random Recipe</button>
        </nav>
    </header>

    <!-- Main Content -->
    <main>
        <aside class="categories">
            <h2>Categories</h2>
            <div id="categoryList"></div>
        </aside>

        <section id="recipeGrid"></section>
    </main>

    <!-- Recipe Modal -->
    <div id="recipeModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <div id="modalContent"></div>
        </div>
    </div>

    <script src="js/api.js"></script>
    <script src="js/script.js"></script>
</body>
</html>
```

### api.js - API Functions
```javascript
// API Configuration
const BASE_URL = 'https://www.themealdb.com/api/json/v1/1';

// API Functions
async function fetchData(endpoint) {
    const response = await fetch(`${BASE_URL}${endpoint}`);
    const data = await response.json();
    return data;
}

// Get random recipe
async function getRandomRecipe() {
    try {
        const data = await fetchData('/random.php');
        return data.meals[0];
    } catch (error) {
        console.error('Error fetching random recipe:', error);
        throw error;
    }
}

// Search recipes
async function searchRecipes(query) {
    try {
        const data = await fetchData(`/search.php?s=${query}`);
        return data.meals || [];
    } catch (error) {
        console.error('Error searching recipes:', error);
        throw error;
    }
}

// Get recipe categories
async function getCategories() {
    try {
        const data = await fetchData('/categories.php');
        return data.categories || [];
    } catch (error) {
        console.error('Error fetching categories:', error);
        throw error;
    }
}

// Get recipe by ID
async function getRecipeById(id) {
    try {
        const data = await fetchData(`/lookup.php?i=${id}`);
        return data.meals[0];
    } catch (error) {
        console.error('Error fetching recipe details:', error);
        throw error;
    }
}
```

### script.js - Main Application Logic
```javascript
// DOM Elements
const searchInput = document.getElementById('searchInput');
const searchBtn = document.getElementById('searchBtn');
const randomRecipeBtn = document.getElementById('randomRecipeBtn');
const recipeGrid = document.getElementById('recipeGrid');
const modal = document.getElementById('recipeModal');
const modalContent = document.getElementById('modalContent');
const closeModal = document.querySelector('.close');
const categoryList = document.getElementById('categoryList');

// Event Listeners
document.addEventListener('DOMContentLoaded', initializeApp);
searchBtn.addEventListener('click', handleSearch);
randomRecipeBtn.addEventListener('click', showRandomRecipe);
closeModal.addEventListener('click', () => modal.style.display = 'none');

// Initialize App
async function initializeApp() {
    try {
        await loadCategories();
        await showRandomRecipe();
    } catch (error) {
        console.error('Error initializing app:', error);
    }
}

// Load Categories
async function loadCategories() {
    try {
        const categories = await getCategories();
        displayCategories(categories);
    } catch (error) {
        console.error('Error loading categories:', error);
    }
}
```

## 3. Step-by-Step Implementation

### Step 1: Basic Styling
Add to style.css:
```css
/* Basic Reset */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    line-height: 1.6;
}

/* Layout */
.recipe-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 20px;
    padding: 20px;
}

/* Recipe Card */
.recipe-card {
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    transition: transform 0.3s ease;
}

.recipe-card:hover {
    transform: translateY(-5px);
}
```

### Step 2: Implement Core Functions
Add to script.js:
```javascript
// Display Recipe Card
function createRecipeCard(recipe) {
    return `
        <div class="recipe-card" onclick="showRecipeDetails(${recipe.idMeal})">
            <img src="${recipe.strMealThumb}" alt="${recipe.strMeal}">
            <div class="recipe-info">
                <h3>${recipe.strMeal}</h3>
                <p>${recipe.strCategory}</p>
            </div>
        </div>
    `;
}

// Show Recipe Details
async function showRecipeDetails(id) {
    try {
        const recipe = await getRecipeById(id);
        displayRecipeModal(recipe);
    } catch (error) {
        console.error('Error showing recipe details:', error);
    }
}

// Handle Search
async function handleSearch() {
    const query = searchInput.value.trim();
    if (query.length === 0) return;

    try {
        const recipes = await searchRecipes(query);
        displayRecipes(recipes);
    } catch (error) {
        console.error('Error handling search:', error);
    }
}
```

### Step 3: Features to Implement
1. Search Functionality
2. Display Recipe Grid
3. Modal Details
4. Category Filtering
5. Loading States
6. Error Handling

## 4. Testing Your Implementation

### API Testing
Test each endpoint in your browser console:
```javascript
// Test random recipe
fetch('https://www.themealdb.com/api/json/v1/1/random.php')
    .then(res => res.json())
    .then(data => console.log(data));

// Test search
fetch('https://www.themealdb.com/api/json/v1/1/search.php?s=chicken')
    .then(res => res.json())
    .then(data => console.log(data));
```

### Features Testing Checklist
- [ ] Search works and displays results
- [ ] Random recipe button works
- [ ] Categories are displayed and clickable
- [ ] Recipe modal shows correct information
- [ ] Loading states are visible
- [ ] Errors are handled gracefully

## 5. Advanced Features to Add

### Local Storage for Favorites
```javascript
// Add to script.js
function addToFavorites(recipeId) {
    let favorites = JSON.parse(localStorage.getItem('favorites')) || [];
    if (!favorites.includes(recipeId)) {
        favorites.push(recipeId);
        localStorage.setItem('favorites', JSON.stringify(favorites));
    }
}
```

### Infinite Scroll
```javascript
// Add to script.js
window.addEventListener('scroll', () => {
    if (window.innerHeight + window.scrollY >= document.body.offsetHeight - 1000) {
        loadMoreRecipes();
    }
});
```

## 6. Common Challenges & Solutions

### Challenge 1: API Response Handling
```javascript
// Handle null responses
async function searchRecipes(query) {
    try {
        const data = await fetchData(`/search.php?s=${query}`);
        return data.meals || [];  // Return empty array if no results
    } catch (error) {
        console.error('Error:', error);
        return [];
    }
}
```

### Challenge 2: Loading States
```javascript
function showLoading() {
    recipeGrid.innerHTML = '<div class="loading">Loading...</div>';
}

function hideLoading() {
    const loading = document.querySelector('.loading');
    if (loading) loading.remove();
}
```

## 7. Best Practices

### Error Handling
```javascript
function showError(message) {
    recipeGrid.innerHTML = `
        <div class="error">
            <p>${message}</p>
            <button onclick="retryLastAction()">Retry</button>
        </div>
    `;
}
```

### Responsive Design
```css
@media (max-width: 768px) {
    .recipe-grid {
        grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    }
}

@media (max-width: 480px) {
    .recipe-grid {
        grid-template-columns: 1fr;
    }
}
```

## 8. Next Steps
1. Add user authentication
2. Implement comments system
3. Add recipe ratings
4. Create meal planner
5. Add nutrition information

Need help with any specific part? Let me know!
