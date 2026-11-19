
# Nema Backend

The Nema backend is built using Node.js and Express.js.
It provides the server-side foundation for the Nema food rescue marketplace.

## Technologies Used

- Node.js
- Express.js
- MongoDB
- Mongoose
- dotenv
- CORS

## Installation

Open a terminal inside the backend folder and run:

npm install

## Running the Server

Start the backend using:

npm start

The server runs on port 3000 by default.

## Health Check

The backend provides a health check endpoint:

GET /api/health

URL:

http://localhost:3000/api/health

Expected response:

{
  "status": "ok"
}

## Main Backend Structure

- server.js: Starts the Express server and defines the health check endpoint.
- db.js: Handles the database connection.
- package.json: Contains project dependencies and scripts.
- package-lock.json: Records the exact dependency versions.

## Environment Variables

The backend uses dotenv to load environment variables.

Create a .env file if required and configure the necessary database settings.

## Development

To run the backend in development mode:

npm run dev
