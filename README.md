# Todo App: Laravel API + Next.js

A todo app split into two parts: a Laravel 10 REST API, and a Next.js front end written in TypeScript that talks to it over HTTP.

```
Todo-App/
├── API/    Laravel 10 REST API (PHP 8.1, MySQL)
└── todo/   Next.js 13 front end (React 18, TypeScript, Tailwind CSS, Axios)
```

## API

| Method | Endpoint | What it does |
| --- | --- | --- |
| GET | `/api/todos` | List todos, newest first |
| POST | `/api/todos` | Create a todo (`title`, `is_done`) |
| PUT/PATCH | `/api/todos/{id}` | Update a todo |
| DELETE | `/api/todos/{id}` | Delete a todo |
| POST | `/api/todos/done/{id}` | Mark a todo done or not done |

It's one resource controller (`TodoController`) with route-model binding, and a migration for the `todos` table.

## Front end

The pages in `todo/pages` call the API through one Axios instance in `todo/lib/axios.js`. It gets the API address from `BACKEND_URL` and sends cookies with each request, so Sanctum login could be added later. Styling is Tailwind CSS.

## Running locally

```sh
# API
cd API
composer install
cp .env.example .env && php artisan key:generate   # set DB_* for your MySQL database
php artisan migrate
php artisan serve                                   # http://127.0.0.1:8000

# Front end (in another terminal)
cd todo
npm install
BACKEND_URL=http://127.0.0.1:8000 npm run dev       # http://localhost:3000
```
