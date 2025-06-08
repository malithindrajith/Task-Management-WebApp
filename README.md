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


SAMPLE CODE FOR THIS PROJECT 




import React, { useState, useEffect } from "react";
import axios from "axios";
import jsPDF from "jspdf";

const Tasks = () => {
  const [tasks, setTasks] = useState([]);
  const [form, setForm] = useState({ title: "", description: "", deadline: "" });

  const fetchTasks = async () => {
    const token = localStorage.getItem("token");
    const res = await axios.get("/api/tasks", {
      headers: { Authorization: `Bearer ${token}` }
    });
    setTasks(res.data);
  };

  const handleCreate = async () => {
    const token = localStorage.getItem("token");
    await axios.post("/api/tasks", form, {
      headers: { Authorization: `Bearer ${token}` }
    });
    setForm({ title: "", description: "", deadline: "" });
    fetchTasks();
  };

  const downloadPDF = () => {
    const doc = new jsPDF();
    doc.text("Task List", 10, 10);
    tasks.forEach((task, i) => {
      doc.text(`${i + 1}. ${task.title} - ${task.status}`, 10, 20 + i * 10);
    });
    doc.save("task-report.pdf");
  };

  useEffect(() => {
    fetchTasks();
  }, []);

  return (
    <div className="p-4">
      <h2 className="text-2xl font-bold mb-4">Tasks</h2>

      <div className="mb-4">
        <input placeholder="Title" value={form.title} onChange={e => setForm({ ...form, title: e.target.value })} className="input" />
        <input placeholder="Description" value={form.description} onChange={e => setForm({ ...form, description: e.target.value })} className="input" />
        <input type="date" value={form.deadline} onChange={e => setForm({ ...form, deadline: e.target.value })} className="input" />
        <button onClick={handleCreate} className="btn mt-2">Create Task</button>
      </div>

      <button onClick={downloadPDF} className="btn mb-2">Download PDF</button>

      <ul>
        {tasks.map(task => (
          <li key={task._id}>{task.title} — {task.status}</li>
        ))}
      </ul>
    </div>
  );
};

export default Tasks;
