# 🚀 Laravel + Inertia.js + Vue 3 + Vite + Tailwind CSS

This project is a full-featured Laravel web application with a Vue 3 frontend powered by Inertia.js, Vite, and Tailwind CSS. Ideal for interactive single-page apps (SPA) with a fast and modern development workflow.

---

## 📁 Project Structure

- `resources/js` — frontend (Vue 3 + Inertia)
- `resources/views/app.blade.php` — entry point for Inertia
- `routes/web.php` — Laravel routes (returning Inertia pages)
- `app/Http/Controllers` — application logic
- `public/` — public assets (output from Vite)

---

## ⚙️ Installation & Setup

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/REPO_NAME.git
cd REPO_NAME

2. Install Laravel dependencies

composer install

3. Install frontend dependencies (Vite + Tailwind)

npm install

4. Copy .env and generate app key

cp .env.example .env
php artisan key:generate

5. Start Laravel development server

php artisan serve

6. Start Vite development server

npm run dev

💡 Useful Commands
Task	Command
Production build	npm run build
Clear all caches	php artisan optimize:clear
Run DB migrations	php artisan migrate
📦 Tech Stack

    Laravel 10+

    Vue 3 (Composition API)

    Inertia.js

    Vite — fast dev server + HMR

    Tailwind CSS — utility-first styling

    Heroicons — modern SVG icon set