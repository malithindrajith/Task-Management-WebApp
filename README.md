# Task-Management-WebApp
The Task Management WebApp is a full-stack application built with the MERN (MongoDB, Express, React, Node.js) stack.


Make sure the following tools are installed:

Node.js 

MongoDB (or MongoDB Atlas for cloud DB)

Git

Vite (used in frontend setup)

Internet access for Gmail/Nodemailer services

steps for run -:

1. Clone the Repository
2. Set Up Environment Variables
3. Install Backend Dependencies
4. Run the Backend Server
5. Install Frontend Dependencies
6. Run the Frontend App
 
Project Root Folder Structure


task-management-webapp/
│
├── backend/                     # Express.js backend
│   ├── controllers/            # All route logic: auth, task, user
│   │   ├── authController.js
│   │   ├── taskController.js
│   │   └── userController.js
│   │
│   ├── models/                 # Mongoose models
│   │   ├── User.js
│   │   └── Task.js
│   │
│   ├── routes/                 # API endpoints
│   │   ├── authRoutes.js
│   │   ├── taskRoutes.js
│   │   └── userRoutes.js
│   │
│   ├── middlewares/           # JWT auth middleware
│   │   └── authMiddleware.js
│   │
│   ├── utils/                 # Utility modules
│   │   └── email.js           # Nodemailer OTP handler
│   │
│   ├── .env.example           # Environment example for backend
│   └── server.js              # Entry point of backend app
│
├── frontend/                   # React frontend (Vite setup)
│   ├── src/
│   │   ├── components/        # Reusable UI components
│   │   │   ├── Header.jsx
│   │   │   ├── ProtectedRoute.jsx
│   │   │   └── TaskItem.jsx
│   │   │
│   │   ├── pages/             # Main pages
│   │   │   ├── Login.jsx
│   │   │   ├── Register.jsx
│   │   │   ├── Dashboard.jsx
│   │   │   ├── Tasks.jsx
│   │   │   └── Profile.jsx
│   │   │
│   │   ├── App.jsx            # App router
│   │   └── main.jsx           # React entry
│   │
│   ├── .env.example           # Environment example for frontend
│   ├── tailwind.config.js     # Tailwind CSS config
│   ├── index.css              # Tailwind base styles
│   └── vite.config.js         # Vite configuration
│
├── env_files.zip              # Zipped environment files for sharing
├── README.md                  # Project overview and instructions
├── .gitignore                 # Ignore node_modules, .env, etc.
└── package.json               # Or separate frontend/backend package.jsons


