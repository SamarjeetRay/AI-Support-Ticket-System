```markdown
# AI Ticket Assistant

An AI-powered ticket management system that automatically categorizes, prioritizes, and assigns support tickets to the most appropriate moderators based on their skills.

## 🚀 Features

### 🤖 AI-Powered Ticket Processing

- Automatic ticket categorization
- Smart priority assignment
- Skill-based moderator matching
- AI-generated helpful notes for moderators

### 👨‍💻 Smart Moderator Assignment

- Automatic matching of tickets to moderators based on skills
- Fallback to admin assignment if no matching moderator is found
- Skill-based routing system

### 👥 User Management

- Role-based access control (User, Moderator, Admin)
- Skill management for moderators
- User authentication with JWT

### ⚡ Background Processing

- Event-driven architecture using Inngest
- Asynchronous ticket processing

## 🛠️ Tech Stack

- **Backend:** Node.js with Express
- **Database:** MongoDB
- **Authentication:** JWT
- **Background Jobs:** Inngest
- **AI Integration:** Google Gemini API
- **Development:** Nodemon

## 📋 Prerequisites

- Node.js (v14 or higher)
- MongoDB
- Google Gemini API key

## ⚙️ Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd ai-ticket-assistant
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Environment Setup

Create a `.env` file in the root directory:

```env
# MongoDB
MONGO_URI=your_mongodb_uri

# JWT
JWT_SECRET=your_jwt_secret

# AI (Gemini)
GEMINI_API_KEY=your_gemini_api_key

# Application
APP_URL=http://localhost:3000
```

## 🚀 Running the Application

### Start the Main Server

```bash
npm run dev
```

### Start the Inngest Development Server

Open another terminal and run:

```bash
npm run inngest-dev
```

The Inngest development server will be available at:

```text
http://localhost:8288
```

## 📝 API Endpoints

### Authentication

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/signup` | Register a new user |
| POST | `/api/auth/login` | Login and get JWT token |

### Tickets

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/tickets` | Create a new ticket |
| GET | `/api/tickets` | Get all tickets for logged-in user |
| GET | `/api/tickets/:id` | Get ticket details |

### Admin

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/auth/users` | Get all users (Admin only) |
| POST | `/api/auth/update-user` | Update user role and skills (Admin only) |

## 🔄 Ticket Processing Flow

### 1. Ticket Creation

- User submits a ticket with a title and description
- System creates the initial ticket record

### 2. AI Processing

- Inngest triggers the `on-ticket-created` event
- AI analyzes the ticket content
- Generates:
  - Required skills
  - Priority level
  - Helpful notes
  - Ticket type

### 3. Moderator Assignment

- System searches for moderators with matching skills
- Uses skill-based matching
- Falls back to admin if no matching moderator is found
- Updates the ticket with the assignment

## 🧪 Testing

### Start the Inngest Development Server

```bash
npm run inngest-dev
```

The Inngest development server will be available at:

```text
http://localhost:8288
```

### Test Ticket Creation

```bash
curl -X POST http://localhost:3000/api/tickets \
-H "Content-Type: application/json" \
-H "Authorization: Bearer YOUR_JWT_TOKEN" \
-d '{
  "title": "Database Connection Issue",
  "description": "Experiencing intermittent database connection timeouts"
}'
```

## 🔍 Troubleshooting

### Port Conflicts

If you see an "address already in use" error:

#### Linux / macOS

```bash
lsof -i :8288
kill -9 <PID>
```

#### Windows PowerShell

```powershell
netstat -ano | findstr :8288
taskkill /PID <PID> /F
```

### AI Processing Errors

- Verify `GEMINI_API_KEY` in `.env`
- Check API quota and limits
- Validate request format
- Check server logs for errors

### MongoDB Connection Issues

- Verify MongoDB is running
- Check the `MONGO_URI`
- Make sure the database is accessible

## 📦 Dependencies

- `@inngest/agent-kit`: `^0.7.3`
- `bcrypt`: `^5.1.1`
- `cors`: `^2.8.5`
- `dotenv`: `^16.5.0`
- `express`: `^5.1.0`
- `inngest`: `^3.35.0`
- `jsonwebtoken`: `^9.0.2`
- `mongoose`: `^8.13.2`
- `nodemailer`: `^6.10.1`

## 🔐 Security

Never commit sensitive credentials to Git.

Add the following to `.gitignore`:

```text
.env
node_modules/
```

## 📄 License

This project is intended for educational and portfolio purposes.
```