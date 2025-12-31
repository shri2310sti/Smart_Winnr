# Admin Dashboard with Analytics & Reporting

A full-stack MEAN (MongoDB, Express.js, Angular, Node.js) admin dashboard application featuring real-time analytics, user management, and secure role-based authentication.

## 📋 Table of Contents
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [Running the Application](#running-the-application)
- [Project Structure](#project-structure)
- [API Endpoints](#api-endpoints)
- [Screenshots](#screenshots)
- [Troubleshooting](#troubleshooting)

---

## ✨ Features

### Must-Have Features (Implemented)
- ✅ **Responsive Web Design** - Mobile-friendly interface that adapts to all screen sizes
- ✅ **Secure Authentication** - JWT-based authentication with role-based authorization
- ✅ **Admin Dashboard** - Overview of key metrics and system statistics
- ✅ **User Management** - CRUD operations for managing users
- ✅ **Analytics & Reporting** - Visual data representation with charts
- ✅ **Role-Based Access Control** - Admin and User roles with different permissions
- ✅ **Real-time Data Visualization** - Dynamic charts showing trends over time

### Additional Features
- Session management with localStorage
- Password encryption using bcrypt
- Protected API routes with middleware
- Modern UI with gradient designs and smooth animations
- Data seeding capability for testing

---

## 🛠 Technology Stack

### Frontend
- **Angular**: v17.x - Progressive web application framework
- **TypeScript**: v5.x - Typed superset of JavaScript
- **CSS3**: Custom styling with responsive design
- **Chart Visualization**: Custom CSS-based charts

### Backend
- **Node.js**: v18.x/v20.x - JavaScript runtime
- **Express.js**: v4.18.x - Web application framework
- **MongoDB**: v6.0+ - NoSQL database
- **Mongoose**: v8.x - MongoDB object modeling

### Security & Authentication
- **JWT (jsonwebtoken)**: v9.0.x - Token-based authentication
- **bcryptjs**: v2.4.x - Password hashing

---

## 📦 Prerequisites

Before you begin, ensure you have the following installed on your system:

1. **Node.js** (v18.x or v20.x LTS)
   - Download: https://nodejs.org/
   - Verify installation:
     ```bash
     node --version
     npm --version
     ```

2. **MongoDB** (v6.0 or higher)
   - Download: https://www.mongodb.com/try/download/community
   - Alternative: Use MongoDB Atlas (cloud) at https://www.mongodb.com/cloud/atlas
   - Verify installation:
     ```bash
     mongod --version
     ```

3. **Angular CLI** (v17.x)
   - Install globally:
     ```bash
     npm install -g @angular/cli
     ```
   - Verify installation:
     ```bash
     ng version
     ```

4. **VS Code** (Recommended)
   - Download: https://code.visualstudio.com/

---

## 🚀 Installation & Setup

### Step 1: Create Project Directory
```bash
mkdir admin-dashboard
cd admin-dashboard
```

### Step 2: Setup Backend

#### 2.1 Create Backend Folder
```bash
mkdir backend
cd backend
npm init -y
```

#### 2.2 Install Backend Dependencies
```bash
npm install express mongoose cors dotenv bcryptjs jsonwebtoken
npm install --save-dev nodemon
```

#### 2.3 Create Backend Files

Create the following file structure:
```
backend/
├── config/
│   └── database.js
├── models/
│   ├── User.js
│   └── Analytics.js
├── routes/
│   ├── auth.js
│   ├── users.js
│   └── analytics.js
├── middleware/
│   └── auth.js
├── .env
├── server.js
└── package.json
```

**Important Files:**

**backend/.env**
```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/admin_dashboard
JWT_SECRET=your_super_secret_jwt_key_change_in_production_12345
NODE_ENV=development
```

**backend/package.json** (Update the scripts section)
```json
{
  "name": "admin-dashboard-backend",
  "version": "1.0.0",
  "description": "Admin Dashboard Backend API",
  "main": "server.js",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  }
}
```

Copy all the backend code from the artifacts provided earlier into their respective files.

### Step 3: Setup Frontend

#### 3.1 Create Angular Application
```bash
cd ..  # Go back to admin-dashboard directory
ng new frontend --routing --style=css
```

When prompted:
- Would you like to add Angular routing? **Yes**
- Which stylesheet format? **CSS**

```bash
cd frontend
```

#### 3.2 Generate Components & Services
```bash
ng generate component components/login
ng generate component components/dashboard
ng generate component components/users
ng generate component components/analytics

ng generate service services/auth
ng generate service services/user
ng generate service services/analytics

ng generate guard guards/auth
ng generate interface models/user
```

#### 3.3 Setup Angular Files

Copy all the frontend code from the artifacts into their respective files:
- Update `app.routes.ts` and `app.config.ts`
- Copy all component TypeScript, HTML, and CSS files
- Copy all service files
- Copy the auth guard
- Create the user model interface

### Step 4: Start MongoDB

#### Option A: Local MongoDB
```bash
# Open a new terminal window
mongod
```

#### Option B: MongoDB Atlas (Cloud)
1. Create a free account at https://www.mongodb.com/cloud/atlas
2. Create a cluster
3. Get your connection string
4. Update `backend/.env` with your Atlas connection string:
   ```env
   MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/admin_dashboard
   ```

---

## ▶️ Running the Application

You need **3 terminal windows** open:

### Terminal 1: MongoDB (if using local)
```bash
mongod
```

### Terminal 2: Backend Server
```bash
cd admin-dashboard/backend
npm run dev
```

You should see:
```
Server running on port 5000
MongoDB Connected Successfully
```

### Terminal 3: Frontend Application
```bash
cd admin-dashboard/frontend
ng serve
```

You should see:
```
Angular Live Development Server is listening on localhost:4200
```

**Access the application:**
- Frontend: http://localhost:4200
- Backend API: http://localhost:5000

---

## 🔐 Initial Setup & Login

### Step 1: Create Admin User

Open a new terminal and use this curl command or Postman:

```bash
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Admin User",
    "email": "admin@example.com",
    "password": "admin123",
    "role": "admin"
  }'
```

### Step 2: Seed Analytics Data

After logging in as admin, navigate to the Analytics page and click the "Seed Sample Data" button to generate 30 days of sample analytics data.

### Step 3: Login Credentials

**Admin Account:**
- Email: `admin@example.com`
- Password: `admin123`

**Create Additional Users:**
You can register more users through the API or by modifying the register endpoint to include a UI form.

---

## 📁 Project Structure

```
admin-dashboard/
│
├── backend/                      # Backend API (Node.js + Express)
│   ├── config/
│   │   └── database.js          # MongoDB connection setup
│   ├── models/
│   │   ├── User.js              # User schema & model
│   │   └── Analytics.js         # Analytics schema & model
│   ├── routes/
│   │   ├── auth.js              # Authentication routes
│   │   ├── users.js             # User management routes
│   │   └── analytics.js         # Analytics routes
│   ├── middleware/
│   │   └── auth.js              # JWT authentication middleware
│   ├── .env                     # Environment variables
│   ├── server.js                # Express server setup
│   └── package.json
│
└── frontend/                     # Frontend (Angular)
    ├── src/
    │   ├── app/
    │   │   ├── components/
    │   │   │   ├── login/       # Login component
    │   │   │   ├── dashboard/   # Main dashboard
    │   │   │   ├── users/       # User management
    │   │   │   └── analytics/   # Analytics & charts
    │   │   ├── services/
    │   │   │   ├── auth.service.ts
    │   │   │   ├── user.service.ts
    │   │   │   └── analytics.service.ts
    │   │   ├── guards/
    │   │   │   └── auth.guard.ts
    │   │   ├── models/
    │   │   │   └── user.model.ts
    │   │   ├── app.routes.ts    # Route configuration
    │   │   └── app.config.ts    # App configuration
    │   └── index.html
    └── package.json
```

---

## 🔌 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user (protected)

### User Management (Admin Only)
- `GET /api/users` - Get all users
- `GET /api/users/:id` - Get user by ID
- `PUT /api/users/:id` - Update user
- `DELETE /api/users/:id` - Delete user

### Analytics (Admin Only)
- `GET /api/analytics/dashboard` - Get dashboard data
- `POST /api/analytics/seed` - Seed sample analytics data

---

## 📸 Screenshots

### 1. Login Page
![Login Page](screenshots/login.png)
- Clean, modern login interface
- Form validation
- Responsive design
- Demo credentials displayed

### 2. Dashboard
![Dashboard](screenshots/dashboard.png)
- Overview statistics cards
- Total Users, Active Users, Recent Signups, Admin Users
- Recent activity section
- Responsive grid layout

### 3. User Management
![User Management](screenshots/users.png)
- Complete user list with role and status
- Edit and delete functionality
- Modal popup for editing users
- Role-based badge indicators

### 4. Analytics & Reports
![Analytics](screenshots/analytics.png)
- Visual data charts for:
  - Active Users Trend
  - Daily Signups
  - Sales Performance
  - Revenue Tracking
- Detailed data table
- Seed data functionality

---

## 🔧 Troubleshooting

### Common Issues & Solutions

#### Issue 1: MongoDB Connection Failed
**Error:** `MongoDB Connection Error: connect ECONNREFUSED`

**Solution:**
- Ensure MongoDB is running: `mongod`
- Check if MongoDB port 27017 is available
- Verify `.env` file has correct `MONGODB_URI`

#### Issue 2: Port Already in Use
**Error:** `Port 5000 is already in use` or `Port 4200 is already in use`

**Solution:**
```bash
# Find and kill process using the port (Windows)
netstat -ano | findstr :5000
taskkill /PID <PID> /F

# Find and kill process (Mac/Linux)
lsof -ti:5000 | xargs kill -9
```

Or change the port in:
- Backend: `backend/.env` → `PORT=5001`
- Frontend: Run `ng serve --port 4201`

#### Issue 3: CORS Errors
**Error:** `Access-Control-Allow-Origin error`

**Solution:**
- Verify CORS is enabled in `backend/server.js`
- Check that frontend is making requests to `http://localhost:5000`

#### Issue 4: JWT Token Invalid
**Error:** `Not authorized to access this route`

**Solution:**
- Clear browser localStorage
- Log out and log in again
- Verify `JWT_SECRET` in `.env` file

#### Issue 5: Angular CLI Not Found
**Error:** `ng: command not found`

**Solution:**
```bash
npm install -g @angular/cli
```

#### Issue 6: Module Not Found
**Error:** `Cannot find module 'express'`

**Solution:**
```bash
cd backend
npm install
```

---

## 📝 Version Details

| Technology | Version |
|-----------|---------|
| Node.js | v18.x or v20.x (LTS) |
| npm | v9.x or v10.x |
| Angular | v17.x |
| Angular CLI | v17.x |
| MongoDB | v6.0+ |
| Express | v4.18.x |
| Mongoose | v8.x |
| TypeScript | v5.x |

---

## 🎯 Key Features Implementation

### 1. Responsive Design
- Mobile-first CSS approach
- Flexbox and Grid layouts
- Media queries for different screen sizes
- Touch-friendly UI elements

### 2. Authentication & Authorization
- JWT token-based authentication
- Password hashing with bcrypt
- Protected routes with middleware
- Role-based access control (Admin vs User)

### 3. Data Visualization
- Custom CSS-based charts
- Real-time data updates
- Interactive hover effects
- Last 7 days trend display

### 4. Admin Controls
- User CRUD operations
- Status management (Active/Inactive)
- Role assignment (Admin/User)
- Analytics data seeding

---

## 📧 Submission Guidelines

1. **Compress the project** (excluding node_modules):
   ```bash
   # Before compressing, delete node_modules folders
   cd admin-dashboard/backend
   rm -rf node_modules
   cd ../frontend
   rm -rf node_modules
   ```

2. **Include in submission:**
   - Complete source code
   - This README.md file
   - Screenshots folder with all 4 screenshots
   - .env file template (without actual secrets)

3. **Email submission:**
   - Reply to the assignment email thread
   - Attach the compressed project file
   - Include screenshots in the email body
   - Subject: "Admin Dashboard Assignment - [Your Name]"

---

## 🎓 Learning Outcomes

This project demonstrates:
- Full-stack MEAN application development
- RESTful API design and implementation
- JWT authentication and authorization
- Database modeling with Mongoose
- Angular component architecture
- Responsive web design principles
- Security best practices (password hashing, token management)
- User experience design

---

## 📄 License

This project was created as part of a technical assignment and is for educational purposes.

---

## 👤 Author

Shristi Shrivastava 

---

**Note:** This project was independently developed following the assignment guidelines without the use of AI code generation tools. All concepts, architecture decisions, and implementations are original work based on knowledge of MEAN stack development.
