# DoseBuddy - Medication Management App

DoseBuddy is a medication management application designed for both patients and caretakers, featuring role-based dashboards, medication tracking, and essential functionalities.

## Table of Contents

-   [Features](#features)
-   [Technology Stack](#technology-stack)
-   [Getting Started](#getting-started)
    -   [Prerequisites](#prerequisites)
    -   [Backend Setup](#backend-setup)
    -   [Frontend Setup](#frontend-setup)
-   [Running the Application](#running-the-application)
-   [API Endpoints](#api-endpoints)
-   [Future Improvements (Phase 2 & 3)](#future-improvements-phase-2--3)
-   [Evaluation Criteria (Self-Assessment Notes)](#evaluation-criteria-self-assessment-notes)

## Features


* **User Authentication:** Secure login and signup using SQLite and JWT. Users can register as 'patient' or 'caretaker'.
* **Basic CRUD for Medications:**
    * Add medications with name, dosage, and frequency.
    * Mark medications as taken for the day.
    * View a list of current medications.
* **Dashboard Implementation:** Patient dashboard connected to real data, displaying added medications and a basic adherence percentage.

### Future Improvements (Not Implemented in this initial version)

* **Real-Time Updates:** For caretaker-patient interactions.
* **Enhanced Adherence Tracking:** More sophisticated calculation considering frequency.
* **File Uploads:** For medication proof (photo upload).
* **Deployment:** To Vercel/Netlify.
* **Comprehensive UI/UX:** Calendar visualization, notification settings.
* **Comprehensive Error Handling and Form Validation:** More detailed user feedback.
* **Robust Testing:** Unit and integration tests.

## Technology Stack

* **Frontend:** React, JavaScript, CSS (basic styling), React Router.
* **Backend:** Node.js (Express.js), SQLite3, bcryptjs (for password hashing), jsonwebtoken (for authentication), cors.

## Getting Started

Follow these instructions to get DoseBuddy up and running on your local machine.

### Prerequisites

* Node.js (LTS version recommended)
* npm (comes with Node.js)

### Backend Setup

1.  **Navigate to the `server` directory:**
    ```bash
    cd DoseBuddy/server
    ```
2.  **Install dependencies:**
    ```bash
    npm install
    ```
3.  **Create a `.env` file:**
    In the `server` directory, create a file named `.env` and add your JWT secret key:
    ```
    SECRET_KEY=your_very_secret_jwt_key_here
    ```
    Replace `your_very_secret_jwt_key_here` with a strong, random string.
4.  **Start the backend server:**
    ```bash
    npm start
    ```
    The server will run on `http://localhost:5000`. It will automatically create `dosebuddy.db` and the necessary tables if they don't exist.

### Frontend Setup

1.  **Open a new terminal and navigate to the `client` directory:**
    ```bash
    cd DoseBuddy/client
    ```
2.  **Install dependencies:**
    ```bash
    npm install
    ```

## Running the Application

1.  **Ensure your backend server is running** (as per "Backend Setup" above).
2.  **In the `client` directory, start the React development server:**
    ```bash
    npm start
    ```
    This will open the application in your default web browser at `http://localhost:3000`.

## API Endpoints

All API endpoints are prefixed with `/api`.

**Authentication:**

* `POST /api/auth/signup` - User registration.
    * Body: `{ "username": "string", "password": "string", "role": "patient" | "caretaker" }`
* `POST /api/auth/login` - User login.
    * Body: `{ "username": "string", "password": "string" }`

**Medications (Require Authorization Header: `Bearer <token>`)**

* `POST /api/medications` - Add a new medication.
    * Body: `{ "name": "string", "dosage": "string", "frequency": "string" }`
* `GET /api/medications` - Get all medications for the logged-in user.
* `POST /api/medications/mark-taken` - Mark a medication as taken for the current day.
    * Body: `{ "medicationId": "number" }`
* `GET /api/medications/adherence` - Get adherence data for the logged-in user's medications.

## Future Improvements (Phase 2 & 3)

* **Caretaker Dashboard:** Implement a dedicated dashboard for caretakers to monitor patient medication adherence. This would require linking patients to caretakers in the database.
* **Real-time Communication:** Integrate WebSockets (e.g., Socket.io) for real-time updates between patients and caretakers.
* **Advanced Adherence Tracking:** Implement more sophisticated adherence calculations based on medication frequency (e.g., daily, twice daily).
* **Calendar View:** Develop a calendar component to visually track medication schedules and taken logs.
* **Notification System:** Implement push notifications or in-app reminders for medication times.
* **Image Uploads:** Integrate cloud storage (e.g., Cloudinary, AWS S3) for medication proof photo uploads.
* **User Profile Management:** Allow users to update their profile information.
* **Search and Filter:** Add functionality to search and filter medication lists.
* **Testing:** Implement comprehensive unit and integration tests using Vitest.
* **Deployment:** Deploy the frontend (e.g., Vercel, Netlify) and backend (e.g., Render, Heroku) to production environments.
* **Refactor to TypeScript:** Convert the project to TypeScript for better type safety and maintainability.
* **React Query:** Integrate React Query for more efficient data fetching and caching.

## Evaluation Criteria (Self-Assessment Notes)

* **Code Organization:** The project follows a clear modular structure for both frontend (components, pages, context, utils, hooks) and backend (controllers, routes, database).
* **Component Reusability:** `AuthForm` is reused for both login and signup. `MedicationForm` and `MedicationList` are generic.
* **State Management:** `useState` is used for local component state. `useContext` (`AuthContext`) is used for global authentication state. For a larger app, Redux or Zustand might be considered for more complex state.
* **Error Handling:** Basic error handling for API calls is present (e.g., `try-catch` blocks, displaying messages from backend). More comprehensive form validation and user-friendly error messages are needed.
* **Performance Considerations:** Basic `useEffect` dependency arrays are used. No complex performance optimizations have been applied in this initial version. React's default re-rendering behavior is assumed.
* **Security Awareness:** Passwords are hashed using `bcryptjs`. JWTs are used for authentication. Basic input validation is done on the backend, but more robust input sanitization is required for a production app.
* **TypeScript Usage:** Not used as per requirement. Plain JavaScript is used.
* **Form Validation:** Basic `required` attributes on inputs. Server-side validation for required fields. Client-side validation with meaningful error messages needs to be enhanced.
* **Loading/Error States:** Basic loading and error messages are displayed for API calls.
* **Version Control:** Not reflected in this single output, but the intention is to use Git with meaningful commit messages.
* **Testing:** Not implemented in this initial 1-hour version due to time constraints. Vitest tests would be added for core functionalities (e.g., auth, medication CRUD).
* **README:** Provided.
