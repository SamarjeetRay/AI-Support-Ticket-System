
# 🎫 AI Ticket Assistant

<p align="center">
  <strong>AI-powered support ticket management system</strong>
</p>

<p align="center">
  Automatically analyze, prioritize, categorize, and assign support tickets to moderators based on their skills.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Node.js-Backend-green?style=for-the-badge&logo=node.js" alt="Node.js"/>
  <img src="https://img.shields.io/badge/Express.js-API-black?style=for-the-badge&logo=express" alt="Express.js"/>
  <img src="https://img.shields.io/badge/MongoDB-Database-green?style=for-the-badge&logo=mongodb" alt="MongoDB"/>
  <img src="https://img.shields.io/badge/Google%20Gemini-AI-blue?style=for-the-badge&logo=google" alt="Gemini"/>
  <img src="https://img.shields.io/badge/Inngest-Background%20Jobs-purple?style=for-the-badge" alt="Inngest"/>
</p>

---

## 📌 About The Project

**AI Ticket Assistant** is a smart ticket management system designed to automate the process of handling customer support requests.

When a user creates a ticket, the system processes the ticket using **Google Gemini AI** to identify important information such as:

- 🎯 Ticket type
- ⚡ Priority level
- 🧠 Required skills
- 📝 Helpful notes for the moderator

Based on the skills identified by the AI, the system searches for suitable moderators and assigns the ticket accordingly.

The ticket-processing workflow is handled asynchronously using **Inngest**.

---

## ✨ Features

### 🤖 AI-Powered Ticket Analysis

- Automatic ticket categorization
- Automatic priority detection
- Required skill identification
- AI-generated moderator notes
- Google Gemini API integration

### 👨‍💻 Intelligent Moderator Assignment

- Skill-based moderator matching
- Automatic ticket routing
- Matching moderators based on required skills
- Admin fallback when no suitable moderator is available

### 🔐 Authentication & Authorization

- JWT-based authentication
- Secure password hashing using bcrypt
- Role-based access control
- Supports:
  - 👤 User
  - 🛠️ Moderator
  - 👑 Admin

### 👥 User Management

- User registration
- User login
- Role management
- Moderator skill management
- Admin-only user management

### ⚡ Event-Driven Processing

- Inngest event-based architecture
- Asynchronous ticket processing
- Background AI processing

---

## 🔄 How It Works

```text
                    👤 USER
                       │
                       ▼
                ┌──────────────┐
                │ Create Ticket│
                └──────┬───────┘
                       │
                       ▼
                ┌──────────────┐
                │   MongoDB    │
                └──────┬───────┘
                       │
                       ▼
                ┌──────────────┐
                │    Inngest   │
                └──────┬───────┘
                       │
                       ▼
                ┌──────────────┐
                │ Google Gemini│
                │      AI      │
                └──────┬───────┘
                       │
             ┌─────────┼─────────┐
             ▼         ▼         ▼
          Category  Priority  Skills
             │         │         │
             └─────────┼─────────┘
                       │
                       ▼
              ┌─────────────────┐
              │    Moderator    │
              │     Matching    │
              └────────┬────────┘
                       │
                ┌──────┴──────┐
                ▼             ▼
          👨‍💻 Moderator    👑 Admin
             Match         Fallback
```

---

## 🧠 AI Processing

When a ticket is created, the AI analyzes its title and description.

### Example

**Input**

```text
Title:
Database Connection Issue

Description:
Experiencing intermittent database connection timeouts.
```

**AI Analysis**

```text
Ticket Type: Technical
Priority: High

Required Skills:
- Database
- Backend

Helpful Notes:
Investigate database connectivity and timeout configuration.
```

The generated information is then used for moderator assignment.

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| **Node.js** | Backend runtime |
| **Express.js** | REST API |
| **MongoDB** | Database |
| **Mongoose** | MongoDB ODM |
| **JWT** | Authentication |
| **bcrypt** | Password hashing |
| **Inngest** | Background processing |
| **Google Gemini** | AI ticket analysis |
| **Nodemon** | Development |

---

## 🏗️ Project Architecture

```text
Client
  │
  ▼
Express.js API
  │
  ├── Authentication
  │
  ├── User Management
  │
  └── Ticket Management
           │
           ▼
        MongoDB
           │
           ▼
        Inngest
           │
           ▼
      Gemini AI
           │
           ▼
  Ticket Analysis
           │
           ▼
Moderator Matching
           │
           ▼
   Ticket Assignment
```

---

## 📋 API Endpoints

### 🔐 Authentication

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/auth/signup` | Register a new user |
| `POST` | `/api/auth/login` | Login and receive JWT token |

### 🎫 Tickets

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/tickets` | Create a new ticket |
| `GET` | `/api/tickets` | Get tickets for logged-in user |
| `GET` | `/api/tickets/:id` | Get ticket details |

### 👑 Admin

| Method | Endpoint | Access |
|--------|----------|--------|
| `GET` | `/api/auth/users` | Admin |
| `POST` | `/api/auth/update-user` | Admin |

---

## 📁 Project Structure

```text
ai-ticket-assistant/
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

Make sure you have the following installed:

- [Node.js](https://nodejs.org/)
- MongoDB
- Git
- Google Gemini API Key

---

### 1️⃣ Clone the Repository

```bash
git clone <repository-url>
cd ai-ticket-assistant
```

### 2️⃣ Install Dependencies

```bash
npm install
```

### 3️⃣ Configure Environment Variables

Create a `.env` file in the root directory.

```env
MONGO_URI=your_mongodb_uri

JWT_SECRET=your_jwt_secret

GEMINI_API_KEY=your_gemini_api_key

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

## 🧪 Test Ticket Creation

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

## 🔒 Environment Variables & Security

Never commit sensitive credentials to GitHub.

Make sure your `.gitignore` contains:

```text
node_modules/
.env
```

Your API keys, database credentials, and JWT secret should always remain private.

---

## 🐛 Troubleshooting

### Port 8288 Already in Use

#### Windows PowerShell

```powershell
netstat -ano | findstr :8288
```

Then terminate the process:

```powershell
taskkill /PID <PID> /F
```

#### Linux / macOS

```bash
lsof -i :8288
kill -9 <PID>
```

### Gemini API Issues

Check:

- `GEMINI_API_KEY` is correctly configured
- Your Gemini API quota
- API request format
- Backend console logs

### MongoDB Issues

Check:

- MongoDB is running
- `MONGO_URI` is correct
- Database connection permissions

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

## 🔮 Future Improvements

Planned improvements may include:

- 📊 Ticket analytics
- 🔎 Advanced ticket search and filtering
- 📈 Moderator workload tracking
- ⚡ Real-time ticket updates
- 🔔 Real-time notifications
- 📝 Ticket history and activity tracking

---

