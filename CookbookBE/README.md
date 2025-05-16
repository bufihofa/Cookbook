<p align="center">
  <a href="http://nestjs.com/" target="blank"><img src="https://nestjs.com/img/logo-small.svg" width="120" alt="Nest Logo" /></a>
</p>

<h1 align="center">Cookbook Backend</h1>

<p align="center">
  Backend service for the Cookbook application, built with <a href="http://nodejs.org" target="_blank">Node.js</a> and the <a href="http://nestjs.com/" target="_blank">NestJS</a> framework. This platform provides a comprehensive set of APIs for managing recipes, users, social interactions, notifications, and AI-powered cooking assistance.
</p>



## 📖 Table of Contents

- [✨ Features](#-features)
- [🛠️ Technologies Used](#️-technologies-used)
- [🏁 Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [⚙️ Environment Variables](#️-environment-variables)
- [🚀 Running the Application](#-running-the-application)
  - [Development Mode](#development-mode)
  - [Watch Mode](#watch-mode)
  - [Production Mode](#production-mode)
- [📄 API Documentation](#-api-documentation)
- [🏗️ Project Structure](#️-project-structure)

## ✨ Features

The Cookbook Backend offers a rich set of features, including:

- **User Management:**
  - User registration with email verification.
  - Secure login with JWT authentication.
  - Password recovery (forgot password and reset password).
  - Secure password change for logged-in users.
  - Profile viewing and updating.
  - User search by username and display name.
- **Post (Recipe) Management:**
  - Create, Read, Update, and Delete (CRUD) operations for posts/recipes.
  - Detailed post information including title, description, cook time, ingredients, and steps.
  - Image uploads associated with posts.
  - Search functionality for posts.
  - View posts by specific users.
- **Social Interactions:**
  - Liking and unliking posts.
  - Commenting on posts (CRUD operations for comments).
  - Liking and unliking comments.
  - Following and unfollowing other users.
  - Viewing followers and following lists.
- **Personalization & Engagement:**
  - Newsfeed generation based on user activity and followed users.
  - Adding/removing posts from a personal "favorites" list.
  - Checking if a post is liked or favorited by the current user.
- **Notifications:**
  - Real-time notifications for various events (e.g., new likes, new comments, new followers).
  - FCM integration for push notifications.
  - Email notifications for critical actions (e.g., verification, password reset, new likes).
  - Viewing and managing notifications (mark as read, delete).
- **AI-Powered Assistance (Cookbook AI Chef):**
  - Analyze an uploaded image of ingredients and suggest recipes that can be made.
  - Generate detailed recipes (ingredients, steps) based on a user-provided list of ingredients and optional dish names.
  - Humorous and engaging recipe instructions.

## 🛠️ Technologies Used

This project leverages a modern stack of technologies:

- **Framework:** [NestJS](https://nestjs.com/) 
- **Language:** [TypeScript](https://www.typescriptlang.org/)
- **Database ORM:** [TypeORM](https://typeorm.io/) 
- **Database:** [MySQL](https://dev.mysql.com/downloads/mysql/8.0.html) 
- **Authentication:** [JSON Web Tokens (JWT)](https://jwt.io/)
- **API Documentation:** [Swagger (OpenAPI)](https://swagger.io/) via NestJS Swagger module
- **Emailing:** [Nodemailer](https://nodemailer.com/) via `@nestjs-modules/mailer`
- **AI API:** [Google Gemini API](https://ai.google.dev/)
- **Push Notifications:** [Firebase Cloud Messaging (FCM)](https://firebase.google.com/docs/cloud-messaging) 
- **Validation:** [class-validator](https://github.com/typestack/class-validator) and [class-transformer](https://github.com/typestack/class-transformer)

## 🏁 Getting Started

Follow these instructions to get the project up and running on your local machine.

### Prerequisites

Ensure you have the following installed:

- [Node.js](https://nodejs.org/) 
- [npm](https://www.npmjs.com/) (comes with Node.js) 
- [MySQL](https://dev.mysql.com/downloads/mysql/8.0.html) 

### Installation

1.  **Clone the repository:**
    ```bash
    git clone <your-repository-url>
    cd CookbookBE
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    ```

3.  **Set up the Database:**
    - Create a new MySQL database (e.g., `cookbook_db`).
    - Ensure your database server is running.

4.  **Configure Environment Variables:**
    - Create a `.env` file in the root of the project by copying the template:
      ```bash
      cp .env.example .env
      ```
    - Update the `.env` file with your specific configurations. See the [Environment Variables](#️-environment-variables) section for details.

5.  **Run Database Migrations (if applicable):**
    If your project uses TypeORM migrations (common practice), run them:
    ```bash
    npm run typeorm:migration:run
    # (The exact command might vary based on your package.json scripts for TypeORM)
    ```
    If not using migrations, TypeORM might synchronize entities if `synchronize: true` is set in development (not recommended for production).

## ⚙️ Environment Variables

The application requires several environment variables to be set. Create a `.env` file in the project root (you can copy `.env.example` if it exists, or create one from scratch).

Below is a template and description of the necessary variables:

```ini
# .env.example - Copy this to .env and fill in your values

# Application Configuration
PORT=3000            

# Database Configuration (PostgreSQL Example)
DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_USERNAME=your_db_user
DATABASE_PASSWORD=your_db_password
DATABASE_NAME=cookbook_db

# JWT Authentication
JWT_SECRET=your_very_strong_and_secret_jwt_key 
JWT_EXPIRATION_TIME=3600s # e.g., 60s, 1h, 7d

# Mailer Configuration (using SMTP)
MAIL_HOST=smtp.example.com
MAIL_PORT=465
MAIL_USER=your_email_username@example.com
MAIL_PASSWORD=your_email_password

# Google Gemini API
GEMINI_API_KEY=your_google_gemini_api_key

```

Ensure these variables are correctly configured before starting the application.

## 🚀 Running the Application

The `package.json` file contains scripts to run and manage the application.

### Development Mode
To run the application in development mode with file watching (restarts on change):
```bash
npm run start:dev
```
The application will typically be available at `http://localhost:PORT` (e.g., `http://localhost:3000`).

### Watch Mode
This is an alias for `start:dev`:
```bash
npm run start --watch
```

### Production Mode
To run the application in production mode:

1.  **Build the application:**
    This compiles TypeScript to JavaScript and copies necessary assets (like email templates).
    ```bash
    npm run build
    ```

2.  **Start the application:**
    ```bash
    npm run start:prod
    ```
    This runs the compiled code from the `dist` folder.


## 📄 API Documentation

API documentation is automatically generated using Swagger (OpenAPI). Once the application is running, you can access the Swagger UI in your browser.

Typically, it's available at: `http://localhost:PORT/api`

The [`AppController`](src/app.controller.ts) serves a landing page at the root (`/`) which links to the API documentation.

## 🏗️ Project Structure

The project follows a standard NestJS structure:

```
CookbookBE/
├── dist/                     # Compiled TypeScript output (after build)
├── node_modules/             # Project dependencies
├── src/                      # Source code
│   ├── app.controller.ts     # Root controller (e.g., for health checks, API docs link)
│   ├── app.module.ts         # Root application module
│   ├── app.service.ts        # Root service
│   ├── main.ts               # Application entry point
│   ├── common/               # Shared resources
│   │   ├── decorators/       # Custom decorators
│   │   ├── filters/          # Exception filters
│   │   ├── guards/           # Authentication/Authorization guards
│   │   ├── interceptors/     # Request/Response interceptors
│   │   ├── middleware/       # Custom middleware
│   │   ├── pipes/            # Data transformation/validation pipes
│   │   └── utils/            # Utility functions
│   ├── config/               # Application configuration
│   │   ├── configuration.ts  # Loads and exposes config variables
│   │   └── validation.schema.ts # Schema for validating .env variables
│   └── modules/              # Feature-specific modules
│       ├── auth/             # Authentication and User management
│       ├── posts/            # Post (Recipe) management
│       ├── follows/          # Follow/Unfollow logic
│       ├── mailer/           # Email sending service and templates
│       │   └── templates/    # Handlebars email templates
│       ├── notifications/    # Notification management
│       └── ...               # Other feature modules
├── test/                     # End-to-end tests
│   ├── app.e2e-spec.ts       # Example e2e test
│   └── jest-e2e.json         # Jest configuration for e2e tests
├── .eslintrc.js              # ESLint configuration
├── .gitignore                # Files and directories to ignore in Git
├── .prettierrc               # Prettier configuration
├── nest-cli.json             # NestJS CLI configuration
├── package.json              # Project dependencies and scripts
├── README.md                 # This file
├── tsconfig.build.json       # TypeScript configuration for building
└── tsconfig.json             # Base TypeScript configuration
```




