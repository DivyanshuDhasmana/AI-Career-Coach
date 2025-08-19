# 🤖 AI Career Coach – Sensai

Sensai is a career guidance application powered by **AI**.  
It helps users explore job roles, prepare for interviews, and gain career insights by leveraging modern **Next.js**, **Clerk authentication**, **AI models**, and **API integrations**.  

---

## 🚀 Project Overview
The **AI Career Coach** project aims to provide:
- Personalized career advice using **AI models**.  
- Secure authentication & user management with **Clerk**.  
- Organized file-based routing in **Next.js 13+ (App Router)**.  
- Middleware integration for protected routes.  
- Modular, clean, and scalable architecture.  

---

## 🛠️ Technologies Used
- **Next.js 13+** → React-based full-stack framework.  
- **Clerk** → Authentication & authorization.  
- **Tailwind CSS** → Styling and responsive UI.  
- **AI APIs (e.g., OpenAI, custom models)** → Intelligent career suggestions.  
- **Middleware** → Protecting routes with server-side checks.  

---

## 📂 File/Folder Structure

sensai/
│── app/ # App Router (Next.js 13+)
│ ├── layout.js # Root layout (shared across pages)
│ ├── page.js # Homepage
│ ├── dashboard/ # Protected career dashboard
│ │ ├── page.js # Dashboard main page
│ │ └── components/ # UI components for dashboard
│ └── api/ # API routes
│ └── career/ # AI-related endpoints
│
│── middleware.js # Clerk authentication middleware
│── package.json # Dependencies & scripts
│── tailwind.config.js # Tailwind CSS configuration
│── .env.local # Environment variables (API keys, Clerk keys)

---

## 🔗 How Files Connect & Their Usage

The **Sensai (AI Career Coach)** project is structured in a modular way so that each file has a clear responsibility.  
Below is the explanation of **how files are connected** and **how they are used** in the project.

---

### 1. **Root Level Files**
- **`package.json`**  
  - Defines project dependencies like `next`, `@clerk/nextjs`, `tailwindcss`.  
  - Contains npm scripts (`dev`, `build`, `start`) that run the app.  

- **`tailwind.config.js`**  
  - Configures **Tailwind CSS** styling system.  
  - Used by all components/pages for responsive UI.  

- **`middleware.js`**  
  - Imports Clerk middleware from `@clerk/nextjs/server`.  
  - Runs **before every request** to check if the user is authenticated.  
  - Example: If a user tries `/dashboard` → `middleware.js` checks login → allows or redirects to login.  

---

### 2. **App Directory (Next.js App Router)**
The `app/` folder is the **heart of the project**. Next.js 13+ uses **file-based routing**, which means each file/folder inside `app/` automatically becomes a route.

#### 📌 `app/layout.js`
- Defines the **root layout** shared across all pages.  
- Imports Clerk providers to manage authentication state globally.  
- Example: When you navigate from `/` to `/dashboard`, `layout.js` ensures header, footer, and styles stay consistent.  

#### 📌 `app/page.js`
- The **landing (homepage)** of the app.  
- Introduces the AI Career Coach concept.  
- Contains links to login/register (via Clerk).  

---

### 3. **Dashboard (Protected Section)**
- **`app/dashboard/page.js`**  
  - The main career guidance interface.  
  - User can enter queries (e.g., “suggest skills for Data Scientist”).  
  - This page **calls API routes** to fetch AI-powered results.  
  - Accessible only if Clerk authentication passes in `middleware.js`.  

- **`app/dashboard/components/`**  
  - Contains reusable UI pieces like career cards, charts, suggestion lists.  
  - Example: `CareerCard.js` may display AI’s suggestions with Tailwind styling.  

---

### 4. **API Routes**
- **`app/api/career/route.js`** (or similar inside `career/`)  
  - Acts as a **mini-backend** inside Next.js.  
  - Handles POST requests coming from `dashboard/page.js`.  
  - Uses AI models (like OpenAI API) to generate responses.  
  - Example Flow:  
    - Dashboard → sends user query to `/api/career`  
    - `route.js` → sends query to AI API → receives response → sends back JSON.  

---

### 5. **Environment Variables (`.env.local`)**
- Stores sensitive keys like Clerk API keys, OpenAI API keys.  
- These are **injected into server files** like `middleware.js` and `api/career/route.js`.  
- Ensures security (keys are not hardcoded in code).  

---

## 🔄 Data & Flow Connection (Step-by-Step)

1. **User visits `/dashboard`**  
   - Request passes through **`middleware.js`**.  
   - If authenticated → continue, else redirect to login.  

2. **`app/layout.js`** loads**  
   - Provides global UI (navbar, providers, etc.).  
   - Makes Clerk session available everywhere.  

3. **`app/dashboard/page.js`** renders**  
   - Shows career input field.  
   - When user asks a query, it calls `fetch('/api/career')`.  

4. **`app/api/career/route.js`** executes**  
   - Reads the request body.  
   - Calls AI API (e.g., OpenAI) with the query.  
   - Returns structured response (career paths, interview prep, skill suggestions).  

5. **`dashboard/page.js`** updates UI**  
   - Receives JSON response from API.  
   - Passes data into UI components (cards, tables, charts).  

6. **Tailwind CSS** styles everything**  
   - Applied across components/pages via `tailwind.config.js`.  

---

✅ This design ensures:
- **Separation of Concerns** (UI, logic, authentication are independent).  
- **Security** (middleware + environment variables).  
- **Scalability** (easily add new APIs like `/api/interview`, `/api/resume`).  

---

## 🛠️ Technologies Used & Why

### ⚡ Next.js 13+ (App Router)
- **Why Used**: Provides a **full-stack React framework** with server-side rendering (SSR), static site generation (SSG), and API routes.  
- **Why Chosen Over Others**:
  - Better performance than plain React (SEO-friendly, fast initial load).  
  - Built-in **App Router** supports modular file-based routing.  
  - Eliminates need for a separate backend (Express/Django) since APIs can live inside `app/api/`.  

---

### 🔐 Clerk (Authentication & Authorization)
- **Why Used**: Simplifies user authentication, signup, and session management with minimal setup.  
- **Why Chosen Over Others**:
  - Easier & faster than Firebase Auth (which is more complex to set up).  
  - More customizable UI than Auth0.  
  - Provides **server-side authentication** compatible with Next.js middleware.  

---

### 🎨 Tailwind CSS
- **Why Used**: Utility-first CSS framework for rapid UI development.  
- **Why Chosen Over Others**:
  - Faster styling compared to writing raw CSS or using SCSS.  
  - More lightweight and customizable than Bootstrap (no heavy pre-built styles).  
  - Responsive design baked in without extra breakpoints setup.  

---

### 🤖 OpenAI API (or any AI API)
- **Why Used**: Powers the **career guidance AI** that generates job suggestions, interview prep, and skill analysis.  
- **Why Chosen Over Others**:
  - State-of-the-art NLP models (GPT-based) → better contextual answers.  
  - More flexible than Dialogflow or Wit.ai (which are intent-based).  
  - Supports creative, open-ended responses, which is perfect for career coaching.  

---

### ⚙️ Middleware (Next.js + Clerk Integration)
- **Why Used**: Ensures only authenticated users can access `/dashboard` and other private routes.  
- **Why Chosen Over Others**:
  - Runs at the **Edge** (very fast, low latency).  
  - No need for separate Express middleware since Next.js handles it natively.  

---

### 📦 Environment Variables (`.env.local`)
- **Why Used**: Keeps sensitive API keys (Clerk, OpenAI) secure and out of source code.  
- **Why Chosen Over Others**:
  - Standard practice in Next.js and Node.js ecosystem.  
  - More secure than hardcoding or storing keys in local config files.  

---

### 🖥️ File-Based Routing (Next.js App Directory)
- **Why Used**: Every file in `app/` automatically becomes a route, making navigation simple and modular.  
- **Why Chosen Over Others**:
  - No need to manually define routes as in Express or older React apps.  
  - Clear separation of pages, APIs, and components → better scalability.  

---

## ✅ Why This Tech Stack Works Well
This combination of tools was chosen because:  
- **Next.js + Clerk** → Full-stack app with secure authentication.  
- **Tailwind CSS** → Speeds up UI development without design complexity.  
- **AI API integration** → Brings intelligence and personalization.  
- **Middleware + API Routes** → Smooth backend logic without needing a separate server.  
- **Scalable & Maintainable** → Easy to extend with new features like interview prep, resume analysis, or job matching.  
