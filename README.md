# 🍬 Sweet Shop Backend

![Sweet Shop Dashboard](./images/sweet-shop-dashboard.png)

This repository contains the backend for the **Sweet Shop** application. It is built using **Node.js**, **Express**, and **MongoDB**, and exposes REST APIs that are consumed by a separate React frontend.

The backend handles user authentication, sweet inventory management, and purchase operations.

---

## 🚀 Features

* User registration and login with JWT authentication
* Add and manage sweets in the database
* List all available sweets
* Purchase sweets and automatically reduce stock
* Basic API testing with Jest and Supertest

---

## 🛠 Tech Stack

* **Node.js** – runtime environment
* **Express.js** – backend framework
* **MongoDB** – database
* **Mongoose** – MongoDB ODM
* **JWT (JSON Web Tokens)** – authentication
* **Jest + Supertest** – testing

---

## 📁 Project Structure

```
sweet-shop/
│
├── server.js                 # Entry point, starts Express server
├── src/
│   ├── config/
│   │   └── db.js              # MongoDB connection setup
│   ├── models/
│   │   ├── User.js            # User schema (name, email, password, role)
│   │   └── Sweet.js           # Sweet schema (name, category, price, quantity)
│   ├── controllers/
│   │   └── authController.js  # Register and login logic
│   ├── routes/
│   │   ├── authRoutes.js      # Auth routes (/api/auth/...)
│   │   └── sweetRoutes.js     # Sweet routes (/api/sweets/...)
│   └── middleware/
│       └── authMiddleware.js  # JWT verification middleware
│
├── tests/
│   └── server.test.js         # Basic health-check test
├── .env                       # Environment variables
├── package.json
└── README.md
```

---

## ⚙️ How to Run the Backend

### 1️⃣ Clone the Repository

```bash
git clone <this-backend-repo-url>
cd sweet-shop
```

### 2️⃣ Install Dependencies

```bash
npm install
```

### 3️⃣ Create `.env` File

Create a `.env` file in the project root and add the following:

```env
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/sweet_shop_db
JWT_SECRET=your_jwt_secret_here
NODE_ENV=development
```

### 4️⃣ Start MongoDB

Make sure MongoDB is running locally or update `MONGO_URI` with your own MongoDB connection string.

### 5️⃣ Run the Server

```bash
npm run dev
```

The backend will be available at:

```
http://localhost:5000
```

---

## 🧪 Running Tests

```bash
npm test
```

---

## 📡 API Endpoints

### 🩺 Health Check

**GET** `/health`

Response:

```json
{
  "status": "ok"
}
```

---

## 🔐 Authentication

### Register User

**POST** `/api/auth/register`

Request Body:

```json
{
  "name": "Test User",
  "email": "test@example.com",
  "password": "password123"
}
```

* Creates a new user
* Password is hashed
* Returns a JWT token

---

### Login User

**POST** `/api/auth/login`

Request Body:

```json
{
  "email": "test@example.com",
  "password": "password123"
}
```

* Validates credentials
* Returns a JWT token

---

## 🍭 Sweets APIs (JWT Required)

All sweets endpoints require the following header:

```
Authorization: Bearer <your_jwt_token>
```

---

### Add a Sweet

**POST** `/api/sweets`

Request Body:

```json
{
  "name": "Gulab Jamun",
  "category": "Classic",
  "price": 20,
  "quantity": 10
}
```

Adds a new sweet to the database.

---

### Get All Sweets

**GET** `/api/sweets`

Returns a list of all available sweets.

---

### Purchase a Sweet

**POST** `/api/sweets/:id/purchase`

* Decreases sweet quantity by 1
* Returns an error if the sweet does not exist or is out of stock

---

## 🖼 Frontend

This backend is designed to work with a separate **React frontend**, which consumes these APIs to display the Sweet Shop dashboard and handle user actions.

---

## ✅ Notes

* Make sure to send the JWT token in protected routes
* MongoDB must be running before starting the server
* Ideal for learning full‑stack authentication and REST API design

---

Feel free to fork, modify, and improve this project 🚀
