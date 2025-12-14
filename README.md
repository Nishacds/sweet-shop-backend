# sweet-shop-backend
Overview
This backend is built with Node.js, Express, and MongoDB.
It exposes a few REST endpoints so a frontend (or tools like Postman) can:

Register and log in users.

Store sweets in a MongoDB collection.

List all sweets and purchase them, reducing the stock.

There is a separate React frontend that calls these APIs.

Tech used
Node.js + Express for the server

MongoDB + Mongoose for the database

JSON Web Tokens (JWT) for authentication

Jest + Supertest for basic testing

Project structure
Main files and folders:

server.js – starts the Express app and connects to MongoDB

src/config/db.js – MongoDB connection setup

src/models/User.js – user schema (name, email, password, role)

src/models/Sweet.js – sweet schema (name, category, price, quantity)

src/controllers/authController.js – register and login logic

src/routes/authRoutes.js – auth endpoints (/api/auth/...)

src/routes/sweetRoutes.js – sweet endpoints (/api/sweets/...)

src/middleware/authMiddleware.js – checks JWT token on protected routes

tests/server.test.js – simple health‑check test

How to run the backend
Clone the repository and go into the folder:

bash
git clone <this-backend-repo-url>
cd sweet-shop
Install dependencies:

bash
npm install
Create a .env file in the project root:

text
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/sweet_shop_db
JWT_SECRET=your_jwt_secret_here
NODE_ENV=development
Start MongoDB (locally or use your own URI in MONGO_URI).

Run the server in development mode:

bash
npm run dev
The backend will be available at http://localhost:5000.

To run the tests:

bash
npm test
API endpoints
Health
GET /health
Simple check that returns { status: "ok" }.

Auth
POST /api/auth/register

Body JSON:

json
{
  "name": "Test User",
  "email": "test@example.com",
  "password": "password123"
}
Creates a new user, hashes the password, and returns a JWT token.

POST /api/auth/login

Body JSON:

json
{
  "email": "test@example.com",
  "password": "password123"
}
Checks the credentials and returns a JWT token if they are valid.

Sweets (require JWT)
All sweets routes require the header:

Authorization: Bearer <token>

You get the token from the login or register response.

POST /api/sweets

Body JSON:

json
{
  "name": "Gulab Jamun",
  "category": "Classic",
  "price": 20,
  "quantity": 10
}
Adds a sweet to the database.

GET /api/sweets

Returns an array of all sweets.

POST /api/sweets/:id/purchase

Decreases quantity by 1 if stock is available.

Returns an error if the sweet does not exist or is out of stock.
