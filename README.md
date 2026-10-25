# 🐞 BugTracker - Real-Time Bug & Issue Tracking System

A full-stack, production-grade **Bug Tracking System** built from scratch using **Node.js, Express.js, MongoDB (Mongoose)** on the backend, and clean, responsive **Vanilla HTML5, CSS3, and JavaScript** on the frontend.

Simulates real-world software development workflows with structured project management: user authentication, bug reporting, triage, status updates, priority filtering, and metrics.

---

## 🌟 Key Features

1. **Authentication & Authorization:**
   - User registration and login with input validation.
   - Secure password hashing using `bcryptjs` with salt rounds.
   - JWT (JSON Web Token) issuance with protected API routes via auth middleware.
   - Persistent session management via `localStorage` with automated session validation (`/api/auth/me`).

2. **Full CRUD Bug Management:**
   - **Report:** Create tickets with Title, Description, Priority (`Low`, `Medium`, `High`), and Status (`Open`, `In Progress`, `Resolved`).
   - **Track:** Real-time dashboard with search, multi-status filtering, priority filtering, and date/priority sorting.
   - **Resolve & Update:** Detailed ticket inspector modal, instant in-place status changer, and complete edit modal.
   - **Delete:** Remove tickets with confirmation alerts.
   - **Ownership & Attribution:** Automatically associates tickets with the creator (`createdBy` referencing the `User` model) and records timestamps.

3. **Dashboard Metrics & Analytics:**
   - Real-time aggregate count cards: **Total**, **Open**, **In Progress**, **Resolved**, and **Critical/High Priority**.
   - Interactive metric cards: Click any stat card to instantly filter tickets by that status.

4. **Modern, Responsive Vanilla UI:**
   - Clean, professional design with dark slate accents and soft shadows.
   - Mobile, tablet, and desktop responsive layouts.
   - Non-blocking toast notification feedback system for all actions.

---

## 📂 Project Directory Structure

```
mp/
├── package.json               # Project manifest, dependencies, scripts
├── package-lock.json
├── .env.example               # Template environment variables
├── .env                       # Local environment configuration
├── .gitignore                 # Ignored files (node_modules, .env, etc.)
├── README.md                  # Complete documentation
│
├── src/                       # Backend Source Code
│   ├── config/
│   │   └── db.js              # Mongoose MongoDB connection & error diagnostics
│   ├── models/
│   │   ├── User.js            # User Schema, bcrypt hashing pre-save hook, matchPassword
│   │   └── Bug.js             # Bug Schema, status/priority enums, user ref
│   ├── middleware/
│   │   └── auth.js            # JWT Bearer token authentication middleware
│   ├── routes/
│   │   ├── authRoutes.js      # Auth API endpoints: /register, /login, /me
│   │   └── bugRoutes.js       # Bug API endpoints: CRUD, /stats, filtering, sorting
│   ├── seed.js                # Database seeding script for sample demo data
│   └── server.js              # Express app entrypoint, middleware, static file serving
│
└── public/                    # Frontend Client Code (Served statically)
    ├── index.html             # Single-Page UI (Auth, Dashboard, Modals)
    ├── css/
    │   └── styles.css         # Modern vanilla CSS styles, cards, badges, toasts
    └── js/
        └── app.js             # Vanilla JS client logic: fetch API, state, event listeners
```

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
| :--- | :--- | :--- |
| **Frontend** | Vanilla HTML5, CSS3, JavaScript (ES6+) | Modern SPA without heavy framework dependencies |
| **Backend** | Node.js, Express.js | RESTful API server and static asset hosting |
| **Database** | MongoDB, Mongoose | NoSQL document database with schema validation |
| **Authentication** | JSON Web Tokens (JWT), `bcryptjs` | Stateless token auth & secure salted password hashing |
| **Tooling** | `dotenv`, `cors`, `nodemon` (node --watch) | Environment configuration and development workflow |

---

## 🚀 Getting Started

### 1. Prerequisites
- **Node.js** (v18 or higher recommended)
- **MongoDB**: Either a local MongoDB instance running on port 27017 or a free cloud cluster from [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).

### 2. Installation
Clone or navigate to the project directory and install dependencies:
```bash
npm install
```

### 3. Environment Configuration
Create or edit your `.env` file in the root directory:
```env
PORT=5000
MONGODB_URI=mongodb://127.0.0.1:27017/bugtracker
JWT_SECRET=super_secret_bugtracker_jwt_key_2026_change_in_production
NODE_ENV=development
```
> *Tip for MongoDB Atlas:* If using Atlas, replace `MONGODB_URI` with your connection string:
> `mongodb+srv://<username>:<password>@cluster0.mongodb.net/bugtracker?retryWrites=true&w=majority`

### 4. Optional: Seed Sample Demo Data
To immediately populate the database with test accounts and realistic bug tickets:
```bash
npm run seed
```
Demo credentials created:
- Email: `sarah@devteam.io`
- Password: `password123`

### 5. Run the Server
Start the production server:
```bash
npm start
```
Or start in development mode with auto-reload:
```bash
npm run dev
```

Open your browser and navigate to:
```
http://localhost:5000
```

---

## 📡 REST API Reference

All protected endpoints require the HTTP header:
`Authorization: Bearer <your_jwt_token>`

### Auth Endpoints (`/api/auth`)

| Method | Endpoint | Access | Description |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/auth/register` | Public | Create new account (`username`, `email`, `password`) |
| `POST` | `/api/auth/login` | Public | Authenticate user & receive JWT token (`email`, `password`) |
| `GET` | `/api/auth/me` | Protected | Get authenticated user profile |

### Bug Endpoints (`/api/bugs`)

| Method | Endpoint | Access | Description |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/bugs/stats` | Protected | Get counts for Total, Open, In Progress, Resolved, High |
| `GET` | `/api/bugs` | Protected | List bugs with query parameters: `status`, `priority`, `search`, `sortBy`, `sortOrder` |
| `GET` | `/api/bugs/:id` | Protected | Get detailed information for a specific bug |
| `POST` | `/api/bugs` | Protected | Create a new bug ticket (`title`, `description`, `priority`, `status`) |
| `PUT` | `/api/bugs/:id` | Protected | Update ticket fields or change status/priority |
| `DELETE` | `/api/bugs/:id` | Protected | Permanently delete a bug ticket |

---

## 🧪 Testing the Application

1. **Sign Up / Sign In:** Create an account or use the seeded demo credentials.
2. **Report a Bug:** Click the **+ Report Bug** button, fill in the title, description, priority, and status, and submit.
3. **Filter & Search:** Type in the search box to find bugs by title or description in real time. Use dropdowns or click the metric cards to filter by status or priority.
4. **View Details & Edit:** Click on any bug card to inspect its full description and reporter details, or click the **Edit** icon to make modifications.
5. **Quick Status Change:** Change a ticket from *Open* to *In Progress* or *Resolved* directly from the dropdown on the card.
6. **Delete:** Click the trash icon to remove a ticket with a confirmation dialog.
