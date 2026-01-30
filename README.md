# 🚦 Smart Traffic Violation Reporting System

A comprehensive web application for reporting and managing traffic violations with role-based access control, built as a final year BTech project.

## 👨‍🎓 Project Information

- **Project Type**: Final Year BTech Project
- **Domain**: Web Development & Public Safety
- **Academic Year**: 2024-2025
- **Technology**: Full Stack Web Application

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [System Architecture](#system-architecture)
- [Installation](#installation)
- [Usage](#usage)
- [API Documentation](#api-documentation)
- [Database Schema](#database-schema)
- [Screenshots](#screenshots)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

The Smart Traffic Violation Reporting System is a web-based platform that enables citizens to report traffic violations by uploading photographic evidence. Administrators can review, verify, and process these reports with automatic penalty assignment based on violation type.

### Problem Statement

Traffic violations are a major cause of road accidents. Traditional reporting methods are cumbersome and time-consuming. This system provides a digital solution for:
- Easy violation reporting by citizens
- Efficient verification by authorities
- Transparent penalty assignment
- Digital record maintenance

### Solution

A user-friendly web application with:
- Simple image-based violation reporting
- Automated penalty calculation
- Role-based access control
- Real-time status tracking

## ✨ Features

### 👤 Citizen Features

- **User Registration & Authentication**
  - Secure account creation
  - JWT-based authentication
  - Password encryption with bcryptjs

- **Violation Reporting**
  - Upload violation images (Base64 encoding)
  - Select violation type from predefined categories
  - Enter location details
  - Automatic date/time recording

- **Dashboard**
  - View all submitted reports
  - Track report status (Pending/Approved/Rejected)
  - View assigned penalties
  - Statistics overview

### 🛡️ Admin Features

- **Admin Panel**
  - View all citizen reports
  - Comprehensive statistics dashboard
  - User management overview

- **Report Verification**
  - Review submitted reports with images
  - Approve or reject reports
  - Automatic penalty assignment on approval

- **Analytics**
  - Total reports count
  - Pending/Approved/Rejected statistics
  - Total penalties collected
  - User registration metrics

### 🔒 Security Features

- JWT authentication with httpOnly cookies
- Password hashing using bcryptjs
- Protected API routes
- Role-based access control (RBAC)
- Input validation on client and server
- Middleware route protection

## 🛠️ Tech Stack

### Frontend
- **Framework**: Next.js 14 (App Router)
- **Language**: JavaScript (ES6+)
- **Styling**: Tailwind CSS
- **UI Components**: Custom React components

### Backend
- **Runtime**: Node.js
- **Framework**: Next.js API Routes
- **Authentication**: JWT (JSON Web Tokens)
- **Password Hashing**: bcryptjs

### Database
- **Database**: MongoDB
- **ODM**: Mongoose
- **Storage**: Base64 image encoding (no external storage)

### Development Tools
- **Package Manager**: npm
- **Code Quality**: ESLint
- **Version Control**: Git

## 🏗️ System Architecture
```
┌─────────────────┐
│   Client        │
│  (React/Next)   │
└────────┬────────┘
         │
         ↓
┌─────────────────┐
│   Next.js       │
│   Middleware    │ ← JWT Validation
└────────┬────────┘
         │
         ↓
┌─────────────────┐
│   API Routes    │
│  (Backend API)  │
└────────┬────────┘
         │
         ↓
┌─────────────────┐
│    MongoDB      │
│   (Database)    │
└─────────────────┘
```

### Data Flow

1. **User Registration**
```
   Client → API → Hash Password → MongoDB → JWT Token → Cookie
```

2. **Report Submission**
```
   Client → Upload Image (Base64) → API → Validate → MongoDB → Response
```

3. **Admin Verification**
```
   Admin → View Report → Approve/Reject → Calculate Penalty → Update DB
```

## 📥 Installation

### Prerequisites

- Node.js (v18 or higher)
- MongoDB (local or MongoDB Atlas)
- npm or yarn

### Step 1: Clone Repository
```bash
git clone https://github.com/yourusername/traffic-violation-system.git
cd traffic-violation-system
```

### Step 2: Install Dependencies
```bash
npm install
```

### Step 3: Environment Configuration

Create a `.env.local` file in the root directory:
```env
MONGODB_URI=mongodb://localhost:27017/traffic-violation
JWT_SECRET=your-super-secret-jwt-key-minimum-32-characters-long
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

**For MongoDB Atlas:**
```env
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/traffic-violation
```

### Step 4: Seed Database (Optional)

Create demo users for testing:
```bash
node scripts/seed.js
```

This creates:
- **Citizen**: citizen@demo.com / password123
- **Admin**: admin@demo.com / admin123

### Step 5: Run Development Server
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Step 6: Build for Production
```bash
npm run build
npm start
```

## 📖 Usage

### For Citizens

1. **Register Account**
   - Navigate to `/register`
   - Fill in name, email, and password
   - Submit to create account

2. **Login**
   - Go to `/login`
   - Enter credentials
   - Redirected to dashboard

3. **Submit Report**
   - Click "Submit Report" button
   - Upload violation image
   - Select violation type:
     - No Helmet (₹1,000)
     - Red Light Jump (₹1,500)
     - Wrong Parking (₹500)
   - Enter location details
   - Submit report

4. **View Dashboard**
   - See all submitted reports
   - Check status and penalties
   - View statistics

### For Administrators

1. **Login with Admin Credentials**
   - Use admin email/password
   - Redirected to admin panel

2. **Review Reports**
   - View all submitted reports
   - Click on any report for details

3. **Verify Reports**
   - Review image and information
   - Click "Approve" to accept and assign penalty
   - Click "Reject" to decline report

4. **Monitor Statistics**
   - Track total reports
   - View pending/approved/rejected counts
   - Monitor penalty collection

## 📡 API Documentation

### Authentication Endpoints

#### Register User
```http
POST /api/auth/register
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123"
}
```

#### Login User
```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "password123"
}
```

#### Logout User
```http
POST /api/auth/logout
```

### Report Endpoints

#### Create Report
```http
POST /api/reports
Authorization: JWT Token (Cookie)
Content-Type: application/json

{
  "image": "data:image/jpeg;base64,...",
  "violationType": "No Helmet",
  "location": "MG Road, Bangalore"
}
```

#### Get User Reports
```http
GET /api/reports
Authorization: JWT Token (Cookie)
```

#### Get All Reports (Admin)
```http
GET /api/reports/all
Authorization: JWT Token (Cookie, Admin Role)
```

### Admin Endpoints

#### Verify Report
```http
PATCH /api/admin/reports/:id/verify
Authorization: JWT Token (Cookie, Admin Role)
Content-Type: application/json

{
  "status": "approved" | "rejected"
}
```

## 🗄️ Database Schema

### User Model
```javascript
{
  _id: ObjectId,
  name: String,           // Required, 2-50 characters
  email: String,          // Required, unique, lowercase
  password: String,       // Required, hashed with bcryptjs
  role: String,           // "citizen" | "admin"
  createdAt: Date         // Auto-generated
}
```

### Report Model
```javascript
{
  _id: ObjectId,
  userId: ObjectId,               // Reference to User
  image: String,                  // Base64 encoded image
  violationType: String,          // Enum: ["No Helmet", "Red Light Jump", "Wrong Parking"]
  location: String,               // Required, 3-200 characters
  date: Date,                     // Auto-captured violation time
  status: String,                 // Enum: ["pending", "approved", "rejected"]
  penalty: Number,                // Auto-assigned based on violation type
  createdAt: Date                 // Auto-generated submission time
}
```

## 💰 Penalty Structure

| Violation Type | Penalty Amount |
|---------------|---------------|
| No Helmet | ₹1,000 |
| Red Light Jump | ₹1,500 |
| Wrong Parking | ₹500 |

Penalties are automatically assigned when an admin approves a report.

## 📸 Screenshots

### Home Page
![Home Page](screenshots/home.png)

### Citizen Dashboard
![Dashboard](screenshots/dashboard.png)

### Report Submission
![Submit Report](screenshots/submit-report.png)

### Admin Panel
![Admin Panel](screenshots/admin-panel.png)

## 🚀 Deployment

### Deploy to Vercel

1. Push code to GitHub
2. Import repository on [Vercel](https://vercel.com)
3. Configure environment variables
4. Deploy

### Environment Variables on Vercel

- `MONGODB_URI`
- `JWT_SECRET`
- `NEXT_PUBLIC_APP_URL`

## 🔮 Future Enhancements

- [ ] Email notifications for report status
- [ ] SMS alerts for citizens
- [ ] Advanced analytics dashboard
- [ ] Export reports to PDF
- [ ] Multi-language support
- [ ] Dark mode theme
- [ ] Mobile application (React Native)
- [ ] Real-time notifications with WebSockets
- [ ] Payment gateway integration for penalties
- [ ] Geolocation auto-capture
- [ ] AI-based violation detection

## 🤝 Contributing

This is an academic project. For suggestions or improvements:

1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

## 👨‍💻 Author

**Your Name**
- Roll Number: [Your Roll Number]
- Department: Computer Science & Engineering
- University: [Your University Name]
- Email: your.email@example.com
- GitHub: [@yourusername](https://github.com/yourusername)

## 🙏 Acknowledgments

- Next.js team for the amazing framework
- MongoDB for the database solution
- Tailwind CSS for styling utilities
- Project guide: [Guide Name]
- Department of CSE, [University Name]

## 📄 License

This project is developed for academic purposes as part of final year BTech curriculum.

---

**⭐ If you found this project helpful, please give it a star!**

---

**Project Status**: ✅ Complete and Production Ready

