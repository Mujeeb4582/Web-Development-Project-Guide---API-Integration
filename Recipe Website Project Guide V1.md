# Recipe Website Project Guide 🍳 V1
A step-by-step guide to build a recipe website using TheMealDB API to master HTML, CSS, and JavaScript.

## 🎯 Project Overview
You'll build a recipe website with features like:
- Search recipes
- Filter by categories
- View recipe details
- Save favorites
- Random recipe generator

## 📁 Project Structure
```
recipe-website/
├── css/
│   └── style.css
├── js/
│   ├── api.js
│   └── script.js
├── images/
└── index.html
```

## 🚀 Step-by-Step Implementation

### Step 1: API Integration
1. First, test these API endpoints in your browser:
```
Random Meal: https://www.themealdb.com/api/json/v1/1/random.php
Search: https://www.themealdb.com/api/json/v1/1/search.php?s=chicken
Categories: https://www.themealdb.com/api/json/v1/1/categories.php
```

2. Create these core functions in api.js:
- fetchRandomRecipe()
- searchRecipes(query)
- getCategories()
- getRecipeById(id)

### Step 2: HTML Structure
Build your HTML in this order:
1. Navigation bar with search
2. Categories sidebar
3. Recipe grid container
4. Recipe modal
5. Loading spinner
6. Error messages

Key HTML concepts to practice:
- Semantic HTML
- Form elements
- Modal structure
- Grid containers

### Step 3: CSS Styling
Style these components in order:

1. Layout:
   - Grid system for recipes
   - Flexbox for navigation
   - Responsive sidebar

2. Components:
   - Recipe cards
   - Search bar
   - Modal
   - Loading spinner

3. Animations:
   - Card hover effects
   - Modal transitions
   - Loading spinner animation

### Step 4: JavaScript Features

Build these features in order:

1. **Basic Data Display**
   - Fetch and display random recipes
   - Create recipe cards
   - Implement loading states

2. **Search Function**
   - Handle search input
   - Update recipe display
   - Add error handling

3. **Category Filtering**
   - Display categories
   - Filter functionality
   - Update UI based on selection

4. **Recipe Details**
   - Modal functionality
   - Display full recipe
   - Ingredient list formatting

5. **Favorites System**
   - Local storage setup
   - Add/remove favorites
   - Favorites page

## 💡 Learning Objectives

### HTML Skills
- [ ] Semantic HTML structure
- [ ] Accessibility attributes
- [ ] Form handling
- [ ] Modal implementation

### CSS Skills
- [ ] Flexbox layouts
- [ ] CSS Grid
- [ ] Responsive design
- [ ] Animations
- [ ] Media queries

### JavaScript Skills
- [ ] API integration
- [ ] Async/await
- [ ] DOM manipulation
- [ ] Event handling
- [ ] Local storage
- [ ] Error handling

## 📝 Implementation Steps

### 1. Basic Setup (Day 1)
```javascript
// Test API connection
async function testAPI() {
    try {
        const response = await fetch('https://www.themealdb.com/api/json/v1/1/random.php');
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error('Error:', error);
    }
}
```

### 2. Core Functions (Day 2-3)
```javascript
// Recipe card template
function createRecipeCard(recipe) {
    // Create card HTML
}

// Display recipes
function displayRecipes(recipes) {
    // Display logic
}

// Search functionality
function handleSearch() {
    // Search logic
}
```

### 3. Features to Add (Day 4-7)
1. Search as you type
2. Category filtering
3. Recipe modal
4. Favorites system
5. Loading states
6. Error handling
7. Responsive design

## 🎯 Challenges to Attempt

1. **Basic Level**
   - Display random recipes
   - Implement search
   - Show recipe details

2. **Intermediate Level**
   - Add category filtering
   - Implement favorites
   - Add loading states
   - Handle errors

3. **Advanced Level**
   - Implement infinite scroll
   - Add print recipe feature
   - Create shopping list
   - Add meal planner

## 🚨 Common Pitfalls to Avoid

1. **API Handling**
   - Not checking for null responses
   - Missing error handling
   - No loading states

2. **UI/UX**
   - Non-responsive design
   - Missing loading indicators
   - Poor error messages

3. **Code Organization**
   - Mixing concerns
   - Duplicate code
   - Poor naming conventions

## ✅ Testing Checklist

### Functionality
- [ ] API calls work
- [ ] Search works
- [ ] Filters work
- [ ] Modal opens/closes
- [ ] Favorites save/load

### Responsiveness
- [ ] Mobile layout works
- [ ] Tablet layout works
- [ ] Desktop layout works

### Error Handling
- [ ] API errors handled
- [ ] No results handled
- [ ] Network errors handled

## 🎨 Styling Ideas

1. **Color Scheme**
```css
:root {
    --primary-color: #ff6b6b;
    --secondary-color: #4ecdc4;
    --background-color: #f7f7f7;
    --text-color: #2d3436;
}
```

2. **Card Design**
```css
.recipe-card {
    border-radius: 8px;
    overflow: hidden;
    transition: transform 0.3s ease;
}
```

3. **Responsive Grid**
```css
.recipes-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 20px;
}
```

## 🚀 Next Steps

After completing the basic project:
1. Add user authentication
2. Implement comments system
3. Add recipe ratings
4. Create meal planner
5. Add nutrition information
6. Implement recipe sharing

## 📚 Resources

1. **API Documentation**
   - [TheMealDB API](https://www.themealdb.com/api.php)

2. **CSS References**
   - [CSS Grid Guide](https://css-tricks.com/snippets/css/complete-guide-grid/)
   - [Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

3. **JavaScript References**
   - [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
   - [Async/Await](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await)

Would you like me to elaborate on any specific part of this guide?
