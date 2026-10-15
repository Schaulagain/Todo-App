# Todo App: Laravel API + Next.js

A full-stack todo app with a **Laravel 10 REST API** back end and a **Next.js + TypeScript** front end, kept as two separate apps that talk over HTTP.

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

Built with a resource controller (`TodoController`), Eloquent route-model binding and a `todos` table migration.

## Front end

Next.js pages in `todo/pages` call the API through a shared Axios instance (`todo/lib/axios.js`). The instance reads the API address from `BACKEND_URL` and sends credentials, so it's ready for Sanctum cookie authentication. Styling is done with Tailwind CSS.

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

## What I learned

* Designing a small REST API in Laravel and consuming it from a separate React/Next.js app.
* Calling an API on a separate origin with a shared Axios client, and typing a front end with TypeScript.
