# Oralvis Healthcare Backend Assignment


## User Credentials

Below are the login credentials for testing the project in live:

### Technician
- **Email:** srinu123@gmail.com  
- **Password:** srinu@2022  

### Dentist
- **Email:** vasu123@gmail.com  
- **Password:** vasu@2022  



## 1. Detailed Feature Breakdown & Step-by-Step Guide

### Part A: Project Setup

- **Backend Setup (Node.js/Express):**
    - Create a new project folder (e.g., `OralVis-Backend-Assignment`).
    - Initialize it as a Node.js project. This will create a `package.json` file.
    - Install the necessary libraries (NPM packages): `express` for the server, `sqlite3` to talk to the database, `cors` to allow your frontend to communicate with your backend, `bcryptjs` to hash passwords securely, `jsonwebtoken` to manage login sessions, `multer` to handle file uploads, and the `cloudinary` SDK.
    - Create your main server file (e.g., `index.js`). Set up a basic Express server that listens for requests.
    - Initialize your SQLite database. You'll need to write SQL statements to create two tables:
        - `users` table: with columns for `id`, `email`, `password` (to store the hashed password), and `role` (`Technician` or `Dentist`).
        - `scans` table: with columns for `id`, `patientName`, `patientId`, `scanType`, `region`, `imageUrl`, and `uploadDate`.

### Part B: Authentication (Login with Roles)

The core of this feature is **Role-Based Access Control (RBAC)**. What a user can see and do depends on their assigned role.

- **Backend API:**
    - Create a `/login` API endpoint.
    - When this endpoint receives an email and password, it should:
        1. Find a user in the `users` table with the matching email.
        2. If the user exists, use `bcryptjs` to compare the provided password with the hashed password stored in the database.
        3. If the password matches, generate a **JSON Web Token (JWT)**. A JWT is like a temporary, secure ID card for the user. Importantly, embed the user's `id` and `role` inside this token.
        4. Send this JWT back to the frontend.

### Part C: Technician – Upload Page

This page is only accessible to users with the "Technician" role.

- **Backend API:**
    - Create a protected `/upload` endpoint that first checks for a valid JWT and verifies the user's role is "Technician".
    - Use the `multer` middleware to process the incoming image file.
    - Use the `cloudinary` SDK to upload the image file to your Cloudinary account.
    - Cloudinary will provide a URL for the successfully uploaded image (e.g., `https://res.cloudinary.com/.../scan123.jpg`).
    - Insert a new record into your `scans` table in the SQLite database, saving all the patient details from the form, the image URL from Cloudinary, and the current timestamp for `uploadDate`.

### Part D: Dentist – Scan Viewer Page

This page is only accessible to users with the "Dentist" role.

- **Backend API:**
    - Create a protected `/scans` endpoint that requires a valid JWT with the "Dentist" role.
    - This endpoint will query your SQLite database and retrieve all records from the `scans` table.
    - It will then send this list of scan data back to the frontend as a JSON array.



## 2. Technologies Used

- Node js
- Express js
- SQLite Database



## 3. Installation setup

#### 1. Clone the repository
```sh
git clone https://github.com/srinivas9548/OralVis-Backend-Assignment.git
cd OralVis-Backend-Assignment
```

#### 2. Install dependencies
```sh
npm install
```

#### 3. Start the server
```sh
npm start
```
