
# 🎫 AI Support Ticket System

<p align="center">
  <strong>AI-powered support ticket management and intelligent moderator assignment</strong>
</p>

<p align="center">
  Automatically categorize, prioritize, and route support tickets to suitable moderators based on their skills.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Node.js-Backend-339933?style=for-the-badge&logo=node.js&logoColor=white" />
  <img src="https://img.shields.io/badge/Express.js-API-000000?style=for-the-badge&logo=express&logoColor=white" />
  <img src="https://img.shields.io/badge/MongoDB-Database-47A248?style=for-the-badge&logo=mongodb&logoColor=white" />
  <img src="https://img.shields.io/badge/Gemini-AI-4285F4?style=for-the-badge&logo=google&logoColor=white" />
  <img src="https://img.shields.io/badge/Inngest-Background%20Jobs-6E56CF?style=for-the-badge" />
</p>

---

## 📌 Overview

**AI Support Ticket System** is a backend application that automates the processing and assignment of customer support tickets.

When a user creates a ticket, the system uses **Google Gemini AI** to analyze the ticket and determine:

- Ticket type
- Priority level
- Required skills
- Helpful notes for the moderator

The system then searches for moderators with matching skills and assigns the ticket accordingly.

Background processing is handled asynchronously using **Inngest**.

---

## ✨ Features

### 🤖 AI-Powered Ticket Processing

- Automatic ticket categorization
- Smart priority assignment
- Required skill identification
- AI-generated helpful notes
- Google Gemini API integration

### 🎯 Smart Moderator Assignment

- Skill-based moderator matching
- Automatic ticket routing
- Matches required ticket skills with moderator skills
- Admin fallback when no suitable moderator is found

### 🔐 Authentication & Authorization

- JWT-based authentication
- Password hashing with bcrypt
- Role-based access control
- Supports User, Moderator, and Admin roles

### 👥 User Management

- User registration
- User login
- Role management
- Moderator skill management
- Admin-only user management

### ⚡ Background Processing

- Event-driven architecture using Inngest
- Asynchronous ticket processing
- Automated AI processing after ticket creation

---

## 🔄 System Workflow

```text
┌──────────────┐
│     User     │
└──────┬───────┘
       │
       │ Create Ticket
       ▼
┌──────────────┐
│   Express    │
│   REST API   │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│   MongoDB    │
│    Ticket    │
└──────┬───────┘
       │
       │ Ticket Created Event
       ▼
┌──────────────┐
│   Inngest    │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ Google Gemini│
│      AI      │
└──────┬───────┘
       │
       ├───────────────┐
       │               │
       ▼               ▼
   AI Analysis    Required Skills
       │               │
       └───────┬───────┘
               ▼
     ┌──────────────────┐
     │    Moderator     │
     │     Matching     │
     └────────┬─────────┘
              │
       ┌──────┴──────┐
       ▼             ▼
  Moderator        Admin
   Match          Fallback
````

---

## 🧠 AI Processing

The AI analyzes the ticket title and description to extract useful information for automated routing.

### Example Ticket

```text
Title:
Database Connection Issue

Description:
Experiencing intermittent database connection timeouts.
```

### AI Output

```text
Ticket Type: Technical
Priority: High

Required Skills:
- Database
- Backend

Helpful Notes:
Investigate the database connection and timeout configuration.
```

This information is then used by the system to find a suitable moderator.

---

## 🛠️ Tech Stack

| Technology        | Purpose               |
| ----------------- | --------------------- |
| **Node.js**       | Backend runtime       |
| **Express.js**    | REST API              |
| **MongoDB**       | Database              |
| **Mongoose**      | MongoDB ODM           |
| **JWT**           | Authentication        |
| **bcrypt**        | Password hashing      |
| **Inngest**       | Background processing |
| **Google Gemini** | AI ticket analysis    |
| **Nodemon**       | Development           |

---

## 🏗️ Architecture

```text
                    ┌─────────────┐
                    │    Client   │
                    └──────┬──────┘
                           │
                           ▼
                    ┌─────────────┐
                    │  Express.js │
                    │     API     │
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
              ▼            ▼            ▼
        Authentication   Tickets      Users
              │            │            │
              └────────────┼────────────┘
                           │
                           ▼
                    ┌─────────────┐
                    │   MongoDB   │
                    └──────┬──────┘
                           │
                           ▼
                    ┌─────────────┐
                    │   Inngest   │
                    └──────┬──────┘
                           │
                           ▼
                    ┌─────────────┐
                    │ Gemini AI   │
                    └──────┬──────┘
                           │
                           ▼
                  Moderator Matching
```

---

## 📋 API Endpoints

### 🔐 Authentication

| Method | Endpoint           | Description             |
| ------ | ------------------ | ----------------------- |
| `POST` | `/api/auth/signup` | Register a new user     |
| `POST` | `/api/auth/login`  | Login and get JWT token |

### 🎫 Tickets

| Method | Endpoint           | Description                        |
| ------ | ------------------ | ---------------------------------- |
| `POST` | `/api/tickets`     | Create a new ticket                |
| `GET`  | `/api/tickets`     | Get tickets for the logged-in user |
| `GET`  | `/api/tickets/:id` | Get ticket details                 |

### 👑 Admin

| Method | Endpoint                | Description                 |
| ------ | ----------------------- | --------------------------- |
| `GET`  | `/api/auth/users`       | Get all users               |
| `POST` | `/api/auth/update-user` | Update user role and skills |

---

## 📁 Project Structure

```text
ai-support-ticket-system/
│
├── src/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── middleware/
│   ├── services/
│   └── ...
│
├── .env
├── .gitignore
├── package.json
├── package-lock.json
└── README.md
```

---

## ⚙️ Getting Started

### Prerequisites

Make sure you have:

* Node.js v14 or higher
* MongoDB
* Git
* Google Gemini API key

### 1. Clone the Repository

```bash
git clone <repository-url>
cd ai-support-ticket-system
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Environment Variables

Create a `.env` file in the root directory:

```env
# MongoDB
MONGO_URI=your_mongodb_uri

# JWT
JWT_SECRET=your_jwt_secret

# Google Gemini
GEMINI_API_KEY=your_gemini_api_key

# Application
APP_URL=http://localhost:3000
```

---

## ▶️ Run the Application

### Start the Backend

```bash
npm run dev
```

The backend will run on:

```text
http://localhost:3000
```

### Start Inngest

Open another terminal:

```bash
npm run inngest-dev
```

The Inngest development dashboard will be available at:

```text
http://localhost:8288
```

---

## 🧪 Testing

### Test Ticket Creation

After logging in and obtaining a JWT token:

```bash
curl -X POST http://localhost:3000/api/tickets \
-H "Content-Type: application/json" \
-H "Authorization: Bearer YOUR_JWT_TOKEN" \
-d '{
  "title": "Database Connection Issue",
  "description": "Experiencing intermittent database connection timeouts"
}'
```

---

## 🔍 Troubleshooting

### Port Conflicts

If port `8288` is already in use:

#### Windows PowerShell

```powershell
netstat -ano | findstr :8288
```

Then:

```powershell
taskkill /PID <PID> /F
```

#### Linux / macOS

```bash
lsof -i :8288
kill -9 <PID>
```

### Gemini API Errors

Check:

* `GEMINI_API_KEY` is correctly configured
* API quota and limits
* Request format
* Backend logs

### MongoDB Connection Errors

Check:

* MongoDB is running
* `MONGO_URI` is correct
* Database access permissions

---

## 📦 Dependencies

```text
@inngest/agent-kit
bcrypt
cors
dotenv
express
inngest
jsonwebtoken
mongoose
nodemailer
```

---

## 🔐 Security

Do not commit sensitive credentials to GitHub.

Add the following to `.gitignore`:

```text
node_modules/
.env
```

Keep the following values private:

```text
MONGO_URI
JWT_SECRET
GEMINI_API_KEY
```

---

## 🚀 Future Improvements

* Advanced ticket filtering
* Ticket analytics
* Real-time ticket updates
* Moderator workload management
* Ticket history and activity tracking
* Improved AI classification
* Advanced moderator matching

---
