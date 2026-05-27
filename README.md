# 404 Found – Lost & Found Management System

A full-stack Lost & Found Management System developed for university campuses to help students report, track, and recover lost items efficiently. The system allows users to report lost or found items, while administrators manage verification, item tracking, and pickup confirmation using secure authentication and MongoDB integration.

---

# Features

* User Registration and Login Authentication
* Report Lost Items
* Report Found Items
* Admin Dashboard for Item Management
* Pickup Code Verification System
* MongoDB Database Integration
* JWT-Based Secure Authentication
* Real-Time Item Tracking and Status Updates
* Search and Manage Reported Items

---

# Technologies Used

## Frontend

* HTML
* CSS
* JavaScript

## Backend

* Node.js
* Express.js

## Database

* MongoDB

## Tools & Platforms

* VS Code
* GitHub
* Postman

---

# Project Structure

```text id="3j86vi"
lost-and-found-system/
│
├── backend/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── scripts/
│   └── server.js
│
├── public/
│
├── package.json
├── package-lock.json
├── README.md
└── .env
```

---

# Installation and Setup

## Step 1 — Clone Repository

```bash id="gmpc22"
git clone https://github.com/thanushree7102/lost-and-found-system.git
```

## Step 2 — Open Project Folder

```bash id="gzt2a0"
cd lost-and-found-system
```

## Step 3 — Install Dependencies

```bash id="d5bm55"
npm install
```

## Step 4 — Configure Environment Variables

Create a `.env` file in the root folder and add:

```env id="jlwm3d"
MONGO_URI=your_mongodb_connection
JWT_SECRET=your_secret_key
PORT=5000
```

---

# Running the Project

## Start Backend Server

```bash id="lqj5hl"
npm start
```

OR

```bash id="4b7z7n"
npm run dev
```

---

# Access the Application

Open browser and visit:

```text id="j51oqn"
http://localhost:5000
```

---

# Demo Admin Credentials

```text id="9c0q8q"
Email: admin@college.edu
Password: admin123
```

---

# Main Functionalities

## User Module

* Register new account
* Login securely
* Report lost items
* Report found items
* Search reported items

## Admin Module

* Verify reported items
* Manage incoming requests
* Generate pickup verification codes
* Update item status
* Monitor item records

---

# API Endpoints

## User APIs

* POST `/api/users/register`
* POST `/api/users/login`

## Item APIs

* POST `/api/items`
* GET `/api/items`
* PUT `/api/items/:id`

---

# Future Enhancements

* QR Code-Based Pickup Verification
* Email Notifications
* AI-Based Item Matching
* Mobile Responsive UI
* React Frontend Integration
* Cloud Deployment

---

# Troubleshooting

## Common Issues

### MongoDB Connection Error

* Ensure MongoDB is running
* Verify `MONGO_URI` inside `.env`

### Failed to Fetch Error

* Ensure backend server is running
* Verify API routes and ports
* Check internet/firewall settings

### Port Already in Use

Change port inside `.env`:

```env id="8m8hln"
PORT=5001
```

---

