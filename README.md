Smart Traffic Violation Reporting System
Project Overview

This is a full-stack Smart Traffic Violation Reporting System built using Next.js (App Router), MongoDB, and Tailwind CSS.
Citizens can report traffic violations, and admins can verify them and assign penalties automatically.

Features
Citizen

Register & Login

Upload traffic violation image

Select violation type: No Helmet, Red Light Jump, Wrong Parking

Auto save location & date

View submitted reports and penalty status

Admin

Secure admin login

View all reports

Approve or reject reports

Auto assign penalties

Penalty System
Violation	Penalty
No Helmet	₹1000
Red Light Jump	₹1500
Wrong Parking	₹500
Tech Stack

Frontend: Next.js (App Router), Tailwind CSS, JavaScript

Backend: Next.js API Routes, MongoDB (Mongoose)

Authentication: JWT (httpOnly cookies)

Password Hashing: bcryptjs

Image Upload: Base64

Installation

Clone the repository:

git clone https://github.com/your-username/smart-traffic-system.git
cd smart-traffic-system


Install dependencies:

npm install


Setup environment variables (.env):

MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
NEXT_PUBLIC_BASE_URL=http://localhost:3000

Running the Project
npm run dev


Frontend & backend are together via Next.js API Routes

Visit: http://localhost:3000

Future Improvements

Real-time location tracking

Automatic image violation detection (AI)

Notifications for citizens about report status

Multi-language support
