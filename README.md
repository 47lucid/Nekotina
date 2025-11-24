# Nekotina

[![Ask DeepWiki](https://devin.ai/assets/askdeepwiki.png)](https://deepwiki.com/47lucid/Nekotina)

Nekotina is a full-stack, real-time chat application built with a modern technology stack. It features a React frontend and a Node.js/Express backend, organized within a Turborepo monorepo. Users can sign up, log in, chat with others in real-time, share images, and customize their profiles and the application's theme.

## Features

-   **User Authentication**: Secure signup, login, and logout functionality using JWTs and `bcrypt` for password hashing.
-   **Real-Time Chat**: Instant messaging between users powered by Socket.IO.
-   **User & Message Management**:
    -   Fetch all registered users to start conversations.
    -   View conversation history with any user.
    -   Send and receive text and image messages.
-   **Cloudinary Integration**: Image messages are uploaded to Cloudinary for efficient storage and delivery.
-   **Online Status**: See which users are currently online or offline.
-   **Profile Customization**: Users can update their profile picture.
-   **Customizable Theming**: A wide variety of themes are available, built with Tailwind CSS and daisyUI, and managed with Zustand.
-   **Responsive UI**: A clean, responsive user interface that works across different screen sizes.

## Tech Stack

-   **Monorepo**: Turborepo
-   **Frontend**:
    -   **Framework**: React (with Vite)
    -   **Styling**: Tailwind CSS, daisyUI
    -   **State Management**: Zustand
    -   **Routing**: React Router
    -   **Real-time Communication**: Socket.IO Client
    -   **HTTP Client**: Axios
-   **Backend**:
    -   **Framework**: Express.js
    -   **Database**: MongoDB with Mongoose
    -   **Real-time Communication**: Socket.IO
    -   **Authentication**: JSON Web Tokens (jsonwebtoken)
    -   **Password Hashing**: bcryptjs
    -   **Image Hosting**: Cloudinary

## Project Structure

The repository is a monorepo managed by Turborepo, containing the following main applications:

```
/
├── apps/
│   ├── backend/      # Express.js REST API and Socket.IO server
│   └── frontend/     # React (Vite) client application
└── packages/
    ├── eslint-config/ # Shared ESLint configuration
    └── typescript-config/ # Shared TypeScript configurations
```

-   `apps/backend`: Handles all server-side logic, including user authentication, message handling, database operations, and WebSocket connections.
-   `apps/frontend`: The user-facing application where users interact with the chat interface.

## Getting Started

Follow these instructions to get a local copy of the project up and running.

### Prerequisites

-   Node.js (v18 or higher)
-   npm (v11 or higher)
-   MongoDB instance (local or Atlas)
-   Cloudinary account for image hosting

### Installation & Setup

1.  **Clone the repository:**
    ```sh
    git clone https://github.com/47lucid/Nekotina.git
    cd Nekotina
    ```

2.  **Install dependencies:**
    This command will install dependencies for the root, frontend, and backend applications.
    ```sh
    npm install
    ```

3.  **Set up environment variables:**
    Create a `.env` file in the `apps/backend` directory and add the following variables:
    ```env
    PORT=5001
    MONGODB_URI=<your_mongodb_connection_string>
    JWT_SECRET=<your_jwt_secret>
    NODE_ENV=development

    # Cloudinary Credentials
    CLOUDINARY_CLOUD_NAME=<your_cloudinary_cloud_name>
    CLOUDINARY_API_KEY=<your_cloudinary_api_key>
    CLOUDINARY_API_SECRET=<your_cloudinary_api_secret>
    ```

4.  **Run the development servers:**
    This command will start both the backend and frontend development servers concurrently.
    ```sh
    npm run dev
    ```
    -   The frontend will be available at `http://localhost:5173`.
    -   The backend server will run on the `PORT` specified in your `.env` file (e.g., `http://localhost:5001`).

### (Optional) Seed the Database

The repository includes a script to seed the database with sample user data.

1.  Navigate to the backend directory:
    ```sh
    cd apps/backend
    ```

2.  Run the seed script:
    ```sh
    node src/seeds/user.seed.js
    ```

## API Endpoints

The backend exposes the following RESTful API endpoints under the `/api` prefix.

### Auth Routes (`/api/auth`)

-   `POST /signup`: Register a new user.
-   `POST /login`: Log in a user and issue a JWT.
-   `POST /logout`: Clear the user's JWT cookie.
-   `GET /check`: Verify the current user's authentication status.
-   `PUT /update-profile`: Update the authenticated user's profile (requires authentication).

### Message Routes (`/api/messages`)

-   `GET /users`: Get a list of all users for the chat sidebar (requires authentication).
-   `GET /:id`: Retrieve the message history with a specific user (requires authentication).
-   `POST /send/:id`: Send a message to a specific user (requires authentication).