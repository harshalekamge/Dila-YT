# Dila-YT — MERN User Management (CRUD Practice)

A beginner **MERN stack** project (MongoDB, Express, React, Node.js) for learning full-stack CRUD: add users, list them, update them and delete them. I built it to practise the stack while preparing for my SLIIT IT Project.

---

## Table of contents

1. [Features](#features)
2. [Tech stack](#tech-stack)
3. [Project structure](#project-structure)
4. [Prerequisites](#prerequisites)
5. [Set up MongoDB](#set-up-mongodb)
6. [Run locally](#run-locally)
7. [API endpoints](#api-endpoints)
8. [Frontend routes](#frontend-routes)
9. [Scripts](#scripts)
10. [Troubleshooting](#troubleshooting)

---

## Features

- **Add user** form — name, email, age, address
- **User details** page listing every user
- **Update user** page
- **Delete** a user
- Navigation bar between Home, User Details and Add User

## Tech stack

| Layer | Technology |
|---|---|
| Frontend | React (Create React App), React Router, Axios |
| Backend | Node.js, Express 4, CORS |
| Database | MongoDB with Mongoose 8 |
| Dev tool | nodemon |

## Project structure

```
Dila-YT/
├── Backend/                         # Express API (port 5000)
│   ├── app.js                       # Server + MongoDB connection
│   ├── Model/UserModel.js           # name, email, age, address
│   ├── Controllers/UserControllers.js
│   ├── Routes/UserRoutes.js         # /users
│   └── package.json
└── frontend/                        # React app (port 3000)
    └── src/
        ├── App.js                   # Routes
        └── Components/
            ├── Nav/                 # Navigation bar
            ├── Home/
            ├── AddUser/
            ├── UserDetails/         # Users list
            ├── User/                # One user row with Update / Delete
            └── UpdateUser/
```

## Prerequisites

| Tool | Version | Check |
|---|---|---|
| Node.js | 18 or newer | `node -v` |
| npm | comes with Node.js | `npm -v` |
| MongoDB | local Community Server, or a free MongoDB Atlas cluster | `mongosh --version` |
| Git | any | `git --version` |

## Set up MongoDB

The connection string is written directly in `Backend/app.js`:

```js
mongoose.connect("<your MongoDB connection string>")
```

Replace it with **your own** connection string:

- **Local MongoDB:** `mongodb://127.0.0.1:27017/dila-yt`
- **MongoDB Atlas:** in Atlas, **Connect → Drivers** and copy the `mongodb+srv://...` string (create a database user and allow your IP under **Network Access**)

> The connection string currently in the file belongs to an old practice Atlas cluster. Change that database user's password in Atlas, and keep connection strings in a `.env` file (with `dotenv`) rather than in code.

## Run locally

```bash
git clone https://github.com/harshalekamge/Dila-YT.git
cd Dila-YT
```

**Backend (terminal 1):**

```bash
cd Backend
npm install
npm start              # nodemon app.js -> http://localhost:5000
```

You should see `Connected to MongoDB`.

**Frontend (terminal 2):**

```bash
cd frontend
npm install
npm start              # http://localhost:3000
```

## API endpoints

Base URL `http://localhost:5000`.

| Method | Route | Body | Action |
|---|---|---|---|
| GET | `/users` | — | List all users |
| POST | `/users` | `{ name, email, age, address }` | Add a user |
| GET | `/users/:id` | — | Get one user |
| PUT | `/users/:id` | `{ name, email, age, address }` | Update a user |
| DELETE | `/users/:id` | — | Delete a user |

Try it:

```bash
curl -X POST http://localhost:5000/users \
  -H "Content-Type: application/json" \
  -d '{"name":"Nimal","email":"nimal@example.com","age":24,"address":"Kandy"}'
```

## Frontend routes

| Route | Page |
|---|---|
| `/`, `/mainhome` | Home |
| `/adduser` | Add user |
| `/userdetails` | All users |
| `/userdetails/:id` | Update a user |

## Scripts

| Folder | Command | What it does |
|---|---|---|
| `Backend/` | `npm start` | Runs the API with nodemon |
| `frontend/` | `npm start` | React dev server |
| `frontend/` | `npm run build` | Production build |

## Troubleshooting

| Problem | Fix |
|---|---|
| `MongooseServerSelectionError` / `bad auth` | Wrong or old connection string — replace it in `Backend/app.js` |
| `querySrv ENOTFOUND` | Atlas address typo, or no internet |
| Atlas: `IP not whitelisted` | Add your IP in Atlas → Network Access |
| Frontend shows no users | Check the backend terminal says `Connected to MongoDB` and runs on port 5000 |

---

Learning project by Harsha Lekamge.
