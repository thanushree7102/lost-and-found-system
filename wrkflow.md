# Workflow and Approach

## Overview
This document explains the approach, web frameworks pipeline, and technologies used in the Lost & Found project. It covers the frontend, backend, and database components, and how they interact to deliver a seamless user experience.

---

## 1. Approach
- **User-Centric Design:** The system is designed for ease of use by students, staff, and administrators.
- **Separation of Concerns:** Frontend, backend, and database are modular, allowing independent development and maintenance.
- **Security:** Pickup codes and admin actions are protected to prevent unauthorized access.
- **Scalability:** RESTful APIs and modular code allow for future expansion (e.g., more campuses, new features).

---

## 2. Web Frameworks Pipeline

### Frontend
- **Framework:** React (Single Page Application)
- **Styling:** Tailwind CSS for rapid, responsive UI development
- **Build Tool:** Babel (for JSX/ES6+ transpilation)
- **Key Features:**
  - Item report/claim forms
  - Search and filter inventory
  - Admin dashboard (client-side demo login)
  - Pickup code generation and validation
  - Bulk delete (delete all items)
  - Hero and background images for branding

### Backend
- **Framework:** Express.js (Node.js)
- **API:** RESTful endpoints for item CRUD, user authentication, and admin actions
- **Security:**
  - JWT-based authentication for admin endpoints
  - Input validation and error handling
- **Key Features:**
  - Item management (add, update, delete, bulk delete)
  - Pickup code persistence
  - Admin and user flows

### Database
- **Database Used:** MySQL
- **Purpose:**
  - Store item records (lost/found status, details, images)
  - Store user/admin credentials
  - Persist pickup codes and claim status
- **Integration:**
  - Backend uses a MySQL client (e.g., `mysql2` or `sequelize`) to interact with the database
  - All item and user actions are reflected in the database for reliability

---

## 3. Pipeline Summary
1. **User submits lost/found item via frontend**
2. **Frontend sends data to backend API**
3. **Backend validates and stores data in MySQL**
4. **Admin reviews and updates item status via dashboard**
5. **Pickup code generated and sent to owner**
6. **Owner claims item at desk; admin verifies code**
7. **Item status updated in database and removed from inventory**

---

## 4. Technologies Used
- **Frontend:** React, Tailwind CSS, Babel
- **Backend:** Node.js, Express.js
- **Database:** Mongo db
- **Other:** REST API, JWT, PowerShell (for local scripts)

---

## 5. Extensibility
- The modular design allows for easy migration to other databases (e.g. PostgreSQL)
- New features (notifications, analytics, etc.) can be added with minimal disruption

---


---

## 6. System Flowchart

Below is a flowchart describing the main workflow of the Lost & Found system:

```mermaid
flowchart TD
  A[User (Student/Staff)] --> B[Report Lost/Found Item]
  B --> C[Item Submitted]
  C --> D[Database (MySQL): Store Item]
  D --> E[Admin Panel: Review Items]
  E --> F{Approve Item?}
  F -- Yes --> G[Item Listed in Inventory/Search]
  F -- No --> H[Item Rejected/Archived]
  G --> I[Owner Claims Item]
  I --> J[Pickup Code Generated]
  J --> K[Owner Visits Desk]
  K --> L[Admin Verifies Code]
  L -- Correct --> M[Item Marked as Returned]
  L -- Incorrect --> J
  M --> N[Item Removed from Inventory]
  %% Optional bulk delete flow
  E -.-> O[Bulk Delete All Items]
  O -.-> P[Database Cleared]
```

---

For more details, see the main project README or contact the project maintainer.
