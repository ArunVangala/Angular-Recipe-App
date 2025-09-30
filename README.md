#🏗️ Project Structure
#recipe-app/
├── src/
│   ├── app/
│   │   ├── models/
│   │   │   └── recipe.model.ts           ✅ Recipe interfaces
│   │   │
│   │   ├── services/
│   │   │   └── recipe.service.ts         ✅ Recipe data & filtering logic
│   │   │
│   │   ├── recipe-list/
│   │   │   ├── recipe-list.component.ts  ✅ Main recipe listing
│   │   │   ├── recipe-list.component.html
│   │   │   └── recipe-list.component.css
│   │   │
│   │   ├── recipe-detail/
│   │   │   ├── recipe-detail.component.ts ✅ Individual recipe view
│   │   │   ├── recipe-detail.component.html
│   │   │   └── recipe-detail.component.css
│   │   │
│   │   ├── recipe-search/
│   │   │   ├── recipe-search.component.ts ✅ Search & filter component
│   │   │   ├── recipe-search.component.html
│   │   │   └── recipe-search.component.css
│   │   │
│   │   ├── app.component.ts              ✅ Root component
│   │   ├── app.component.html
│   │   ├── app.component.css
│   │   ├── app.config.ts                 ✅ App configuration
│   │   └── app.routes.ts                 ✅ Routing configuration
│   │
│   ├── styles.css                        ✅ Global styles
│   └── index.html
│
└── package.json



🔗 Component Relationships
Data Flow Architecture
RecipeService (Single Source of Truth)
    ↓
    ├── filteredRecipes$ (Observable)
    │   ↓
    │   └── RecipeListComponent (Displays filtered recipes)
    │       └── RecipeSearchComponent (Updates filters)
    │
    └── getRecipeById()
        ↓
        └── RecipeDetailComponent (Shows single recipe)
Component Hierarchy
AppComponent (Root)
├── Header (Navigation)
├── Router Outlet
│   ├── RecipeListComponent (Path: '/')
│   │   ├── RecipeSearchComponent
│   │   └── Recipe Cards (Grid)
│   │
│   └── RecipeDetailComponent (Path: '/recipe/:id')
│       └── Recipe Details
│
└── Footer


🚀 Key Features
1. Recipe Service (recipe.service.ts)

Centralized data management using RxJS BehaviorSubject
Real-time filtering with combineLatest
Filters: search term, category, cuisine, difficulty
Sample data with 6 recipes (easily expandable)

2. Recipe List (recipe-list.component)

Grid layout with responsive design
Recipe cards with hover effects
Rating display with star icons
Quick stats (time, servings, calories)
Click to view detailed recipe

3. Recipe Search (recipe-search.component)

Search input with real-time filtering
Dropdown filters: Category, Cuisine, Difficulty
Reset filters button
Two-way data binding with FormsModule

4. Recipe Detail (recipe-detail.component)

Full recipe information
Hero image with badges
Comprehensive stats section
Ingredients checklist
Step-by-step instructions
Tags display
Back navigation

5. App Component (app.component)

Sticky header with logo
Navigation links
Footer with social links
Gradient background

🎨 Design Features

Modern UI: Clean, professional design with gradients
Responsive: Mobile-first approach, works on all devices
Animations: Smooth transitions and hover effects
Color Scheme: Purple gradient (#667eea to #764ba2)
Icons: Custom SVG icons throughout
Typography: System fonts for optimal performance

📱 Routing Configuration
typescriptRoutes:
- '/' → RecipeListComponent (Home page with all recipes)
- '/recipe/:id' → RecipeDetailComponent (Individual recipe)
- '**' → Redirect to '/' (404 handling)
🔧 Installation & Setup
1. Create the files in your Angular project:
bash# Models
src/app/models/recipe.model.ts

# Services
src/app/services/recipe.service.ts

# Components
src/app/recipe-list/
src/app/recipe-detail/
src/app/recipe-search/

# Root files
src/app/app.component.ts
src/app/app.component.html
src/app/app.component.css
src/app/app.routes.ts
2. Ensure app.config.ts includes routing:
typescriptimport { ApplicationConfig, provideZoneChangeDetection } from '@angular/core';
import { provideRouter } from '@angular/router';
import { routes } from './app.routes';

export const appConfig: ApplicationConfig = {
  providers: [
    provideZoneChangeDetection({ eventCoalescing: true }),
    provideRouter(routes)
  ]
};
3. Update styles.css with global styles
4. Run the application:
bashng serve
Visit: http://localhost:4200
🎯 Usage Examples
Adding a New Recipe
Edit recipe.service.ts:
typescriptprivate recipes: Recipe[] = [
  // ... existing recipes
  {
    id: 7,
    name: 'Your New Recipe',
    description: 'Description here',
    category: 'Main Course',
    cuisine: 'Italian',
    prepTime: 15,
    cookTime: 30,
    servings: 4,
    difficulty: 'Medium',
    imageUrl: 'https://example.com/image.jpg',
    ingredients: ['ingredient 1', 'ingredient 2'],
    instructions: ['step 1', 'step 2'],
    rating: 4.5,
    calories: 400,
    tags: ['tag1', 'tag2']
  }
];
Customizing Filters
The service automatically extracts unique categories and cuisines from recipes. Just add recipes with new values!
🧩 Component Communication

RecipeSearchComponent → RecipeService: Updates filters
RecipeService → RecipeListComponent: Provides filtered recipes
RecipeListComponent → Router: Navigates to detail page
RecipeDetailComponent → RecipeService: Fetches specific recipe

📊 Data Model
typescriptinterface Recipe {
  id: number;
  name: string;
  description: string;
  category: string;          // Main Course, Salad, Dessert
  cuisine: string;           // Italian, Indian, Mexican, etc.
  prepTime: number;          // minutes
  cookTime: number;          // minutes
  servings: number;
  difficulty: 'Easy' | 'Medium' | 'Hard';
  imageUrl: string;
  ingredients: string[];
  instructions: string[];
  rating: number;            // 0-5
  calories: number;
  tags: string[];
}
🎓 Learning Points
This project demonstrates:
Standalone Components (Angular 18+)
RxJS Observables (BehaviorSubject, combineLatest)
Reactive Filtering (Real-time search)
Component Communication (Service pattern)
Angular Router (Navigation & params)
Responsive Design (Mobile-first CSS)
Modern CSS (Gradients, animations, grid)

🚦 Next Steps / Enhancements
Add favorites/bookmarking
Implement recipe ratings
Add print recipe functionality
Include nutritional information
Add cooking timer
Implement recipe comments
Connect to a backend API
Add user authentication
Enable recipe submission

📝 Notes
All components are standalone (no NgModule needed)
Uses Angular 18 features
No external UI libraries (pure CSS)
Responsive and mobile-friendly
Production-ready code structure

Happy Coding! 🍳
