## 404 Found Lost & Found — Quickstart & Interactive Guide

Welcome! This README gives you a short, interactive set of steps to run and test the Lost & Found app locally, plus quick pointers for common tasks and troubleshooting.

---

## Interactive Checklist
Use this list as a small hands-on guide — tick the boxes as you complete them.

- [ ] Prerequisites installed: Node.js (16+), MongoDB running
- [ ] Environment configured (`.env` with MONGO_URI, JWT_SECRET, PORT)
- [ ] Start the server and confirm the site responds at http://localhost:5000
- [ ] Run admin setup script (`backend/scripts/setupAdmin.js`) to ensure admin exists
- [ ] Report an item via the UI (Found or Lost) and confirm it appears in admin Incoming Drop-off Alerts
- [ ] Verify pickup code flow (generate → persist → verify at terminal)

Tip: You can update this file locally and check items as you go.

---

## Quick Start (Windows PowerShell)

1. Open PowerShell and cd into the project root (the folder that contains this README):

```powershell
cd "H:\Group project"
```

2. Install (if needed) — this project currently relies on the backend only. If you need to add packages, run:

```powershell
# (optional) npm install
npm install
```

3. Start the backend server:

```powershell
npm start
```

4. Confirm the site responds:

```powershell
Invoke-WebRequest http://localhost:5000 -UseBasicParsing | Select-Object -First 1
```

If you get StatusCode 200 and HTML content, the site is up.

---

## Ensure admin account exists
Run the helper script to create or confirm the admin account used by the demo flows:

```powershell
node "backend/scripts/setupAdmin.js"
```

Expected output: messages indicating the script connected to MongoDB and that the admin account exists or was created.

Default demo admin credentials (if created by the script):
- email: admin@college.edu
- password: admin123

Note: The demo flows may also include a one-click admin fallback; use the UI button if present.

---

## Useful API endpoints (local testing)
These are the main endpoints used by the frontend. They are protected by JWT where indicated.

- POST /api/users/register — create user
- POST /api/users/login — authenticate and receive JWT
- POST /api/items — create an item (protected for certain flows)
- GET /api/items — list/search items
- PUT /api/items/:id — update item fields (e.g., persist pickupCode)

You can test endpoints with PowerShell like this:

```powershell
#$json = @{email="admin@college.edu"; password="admin123"} | ConvertTo-Json
Invoke-WebRequest -Uri http://localhost:5000/api/users/login -Method POST -ContentType "application/json" -Body $json -UseBasicParsing | Select-Object -ExpandProperty Content
```

---

## Typical user flows to test (manual)

1. Reporter Flow (Found Item)
   - Open the app in a browser: http://localhost:5000
   - Submit a "Found" report. The frontend sets found items to status `pending_dropoff` so admins see them in Incoming Drop-off Alerts.

2. Admin Flow (Incoming Drop-off Alerts)
   - Log in as admin (or use one-click demo admin)
   - Confirm incoming drop-offs. The system generates/persists pickup codes and moves items to `at_desk` or another state depending on your action.

3. Claim Flow (Picker)
   - The picker provides the pickup code to claim their item. The terminal UI verifies the code vs persisted `pickupCode` on the item.

---

## Where to look and small dev notes

- Frontend single-file SPA: `public/index.html` (this was copied from the original `Lost and Found.html`).
- Server entrypoint: `backend/server.js` (start script points here).
- Item logic & persistence: `backend/controllers/itemController.js` and `backend/models/Item.js` (pickupCode field is present and marked unique/sparse).

Pickup code generation: the app currently uses a deterministic hash-based generator so codes are stable per item. If you want pickup codes to be generated on the server instead, move the generator into `backend/controllers/itemController.js` and persist the value when creating/updating the item.

---

## Troubleshooting

- Server not reachable: ensure MongoDB is running and `.env` MONGO_URI points to the right instance.
- MongoDB connection errors: check `backend/server.js` logs, the console will show connection attempts.
- CORS / network issues: the server sets permissive CORS for local dev but if you modified headers, ensure the frontend can call `/api`.
- Admin login fails with "User already exists": run `node backend/scripts/setupAdmin.js` to reconcile the admin user.

If something is broken after edits, run the server in the terminal directly so you can see logs:

```powershell
cd "H:\Group project"
npm start
```

Watch the terminal for messages like "Server running on port 5000" and "MongoDB connected".

---

## Quick contribution / dev checklist

If you want to extend the project, here are low-risk tasks to pick from:

- [ ] Move pickup code generation to server and add tests for uniqueness.
- [ ] Persist `at_desk` status and `droppedBy` metadata on confirm (server-side).
- [ ] Add small unit tests for `backend/controllers/itemController.js` (jest/mocha).
- [ ] Improve UI by extracting `public/index.html` into modular files (React app build) and adding a build step.

---

## Final notes
If you prefer I continue with the repo reorganization (move originals into `archive/` and ensure server serves `public/` by default) tell me "reorganize" and I will: copy/move files, update `backend/server.js` static serving if needed, and run a quick verification.

If you want me to run the admin setup or try an admin login now, say "admin" or "login".

Thanks — go ahead and tick the checklist above as you work through the steps!
