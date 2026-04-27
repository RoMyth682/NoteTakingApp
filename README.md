# 📝 NoteTakingApp

A full-stack MERN note-taking application with Redis-powered rate limiting, built for creating, reading, updating, and deleting notes.

## 🚀 Tech Stack

### Frontend
- **React 19** (Vite)
- **Tailwind CSS** + **DaisyUI**
- **React Router v7** — client-side routing
- **Axios** — HTTP requests
- **React Hot Toast** — toast notifications
- **Lucide React** — icons

### Backend
- **Node.js** + **Express.js**
- **MongoDB** + **Mongoose**
- **Upstash Redis** + **@upstash/ratelimit** — serverless rate limiting (sliding window: 10 requests / 20 seconds)

---

## ✨ Features

- 📄 Create, view, edit, and delete notes
- 🔒 Redis-powered rate limiting on all API endpoints to prevent spam/abuse
- 💾 Client-side caching with localStorage — notes persist on page refresh
- 🔔 Toast notifications for success, errors, and rate limit warnings
- ⚡ Fast load times with Vite

---

## 📁 Project Structure

```
NoteTakingApp/
├── backend/
│   └── src/
│       ├── config/
│       │   ├── db.js           # MongoDB connection
│       │   └── upstash.js      # Upstash Redis rate limiter config
│       ├── controllers/
│       │   └── notesController.js
│       ├── middleware/
│       │   └── rateLimiter.js
│       ├── models/
│       │   └── Note.js
│       ├── routes/
│       │   └── notesRoutes.js
│       └── server.js
└── frontend/
    └── src/
        ├── components/
        │   ├── Navbar.jsx
        │   ├── NoteCard.jsx
        │   ├── NotesNotFound.jsx
        │   └── RateLimitedUI.jsx
        ├── lib/
        │   ├── axios.jsx
        │   └── utils.jsx
        └── pages/
            ├── HomePage.jsx
            ├── CreatePage.jsx
            └── NoteDetailPage.jsx
```

---

## ⚙️ Environment Variables

Create a `.env` file inside the `backend/` folder:

```env
MONGO_URI=your_mongodb_connection_string
PORT=5001

UPSTASH_REDIS_REST_URL=your_upstash_redis_url
UPSTASH_REDIS_REST_TOKEN=your_upstash_redis_token
```

> ⚠️ Never commit your `.env` file — it is already included in `.gitignore`

To get your Upstash credentials:
1. Go to [upstash.com](https://upstash.com) and create a free Redis database
2. Copy the `UPSTASH_REDIS_REST_URL` and `UPSTASH_REDIS_REST_TOKEN` from the dashboard

---

## 🛠️ Getting Started

### Prerequisites
- Node.js installed
- MongoDB Atlas account (or local MongoDB)
- Upstash account (free tier is enough)

### 1. Clone the repository
```bash
git clone https://github.com/RoMyth682/NoteTakingApp.git
cd NoteTakingApp
```

### 2. Install backend dependencies
```bash
cd backend
npm install
```

### 3. Install frontend dependencies
```bash
cd ../frontend
npm install
```

### 4. Set up environment variables
```bash
# Inside backend/ create a .env file and add:
MONGO_URI=your_mongodb_connection_string
PORT=5001
UPSTASH_REDIS_REST_URL=your_upstash_redis_url
UPSTASH_REDIS_REST_TOKEN=your_upstash_redis_token
```

### 5. Run the backend
```bash
cd backend
npm run dev
```

### 6. Run the frontend
```bash
cd frontend
npm run dev
```

### 7. Open in browser
```
http://localhost:5173
```

---

## 🛡️ Rate Limiting

Powered by **Upstash Redis** with a sliding window algorithm:

| Config | Value |
|--------|-------|
| Strategy | Sliding Window |
| Limit | 100 requests |
| Window | 60 seconds |
| Scope | All API endpoints |

When rate limited, the app returns a `429` status. The frontend handles this gracefully — the UI never resets or goes blank, and a toast notification is shown to the user.

---

## 🔌 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/notes` | Get all notes |
| GET | `/api/notes/:id` | Get a single note |
| POST | `/api/notes` | Create a new note |
| PUT | `/api/notes/:id` | Update a note |
| DELETE | `/api/notes/:id` | Delete a note |

---

## 🙏 Credits

This project was built by following the [MERN Stack Tutorial for Beginners with Deployment – 2025](https://www.youtube.com/watch?v=F9gB5b4jgOI) by [freeCodeCamp](https://www.freecodecamp.org).

Additional improvements made on top of the tutorial:
- localStorage caching to prevent blank page on rate limit
- Graceful 429 error handling in NoteDetailPage
- Toast notifications without UI reset on refresh
