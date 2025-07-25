# React BlogSpace 🚀

[![React](https://img.shields.io/badge/React-18.0.0-blue.svg)](https://reactjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0.0-blue.svg)](https://www.typescriptlang.org/)
[![Node.js](https://img.shields.io/badge/Node.js-18.0.0-green.svg)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-4.18.0-gray.svg)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-6.0.0-green.svg)](https://www.mongodb.com/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.3.0-blue.svg)](https://tailwindcss.com/)
[![Vite](https://img.shields.io/badge/Vite-4.4.0-purple.svg)](https://vitejs.dev/)

A modern, full-stack blog platform built with React, TypeScript, and Node.js. Features a rich markdown editor, file management system, and JWT authentication.

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [API Documentation](#-api-documentation)
- [Development](#-development)
- [Deployment](#-deployment)
- [Contributing](#-contributing)
- [License](#-license)

## ✨ Features

### 🎨 Frontend Features
- **Modern UI/UX**: Clean, responsive design with Tailwind CSS
- **Rich Text Editor**: Markdown editor with live preview
- **File Management**: Virtual file system for organizing documents
- **Authentication**: Secure login/register with JWT tokens
- **Real-time Updates**: Live preview and auto-save functionality
- **Responsive Design**: Works seamlessly on desktop and mobile

### 🔧 Backend Features
- **RESTful API**: Express.js server with structured endpoints
- **Authentication**: JWT-based user authentication and authorization
- **Database**: MongoDB integration with Mongoose ODM
- **File Operations**: CRUD operations for blogs and files
- **Security**: Input validation and sanitization
- **Analytics**: Blog view tracking and analytics

### 🛠️ Development Features
- **Hot Reload**: Automatic server restart on file changes
- **TypeScript**: Full type safety across the application
- **ESLint**: Code quality and consistency
- **Vite**: Fast development and build times
- **Modular Architecture**: Clean separation of concerns

## 🛠️ Tech Stack

### Frontend
- **React 18** - UI library
- **TypeScript** - Type safety
- **Tailwind CSS** - Styling framework
- **Vite** - Build tool and dev server
- **React Router** - Client-side routing
- **Axios** - HTTP client

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - NoSQL database
- **Mongoose** - ODM for MongoDB
- **JWT** - Authentication tokens
- **bcryptjs** - Password hashing
- **cors** - Cross-origin resource sharing

### Development Tools
- **ESLint** - Code linting
- **Nodemon** - Auto-restart server
- **Git** - Version control

## 📁 Project Structure

```
wordloom/
├── backend/                 # Express.js API server
│   ├── controllers/        # Route controllers
│   │   ├── authController.js
│   │   ├── blogController.js
│   │   └── fileController.js
│   ├── middleware/         # Custom middleware
│   │   └── auth.js
│   ├── models/            # MongoDB schemas
│   │   ├── Blog.js
│   │   ├── User.js
│   │   ├── File.js
│   │   └── Folder.js
│   ├── routes/            # API routes
│   │   ├── auth.js
│   │   ├── blogs.js
│   │   └── files.js
│   ├── server.js          # Main server file
│   └── package.json
├── frontend/              # React + Vite client
│   ├── src/
│   │   ├── components/    # React components
│   │   │   ├── Auth/     # Authentication components
│   │   │   ├── Editor/   # Markdown editor
│   │   │   ├── FileExplorer/ # File management
│   │   │   ├── Preview/  # Blog preview
│   │   │   ├── Sidebar/  # Navigation sidebar
│   │   │   └── UI/       # Reusable UI components
│   │   ├── contexts/     # React contexts
│   │   ├── hooks/        # Custom React hooks
│   │   ├── pages/        # Page components
│   │   ├── services/     # API services
│   │   └── types/        # TypeScript type definitions
│   ├── public/           # Static assets
│   └── package.json
├── package.json           # Root package.json
└── README.md             # This file
```

## 📋 Prerequisites

Before running this project, make sure you have the following installed:

- **Node.js** (v18 or higher)
- **npm** (v8 or higher)
- **MongoDB** (v6 or higher)

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/Rishant12220055/Blog_Website.git
cd Blog_Website
```

### 2. Install Dependencies

Install all dependencies for the root project, backend, and frontend:

```bash
npm run install:all
```

This command will install dependencies for:
- Root project
- Backend (Express.js server)
- Frontend (React application)

## ⚙️ Configuration

### Environment Variables

Create a `.env` file in the `backend` directory:

```env
# Server Configuration
PORT=5000
NODE_ENV=development

# MongoDB Configuration
MONGODB_URI=mongodb://localhost:27017/blogspace

# JWT Configuration
JWT_SECRET=your_jwt_secret_key_here
JWT_EXPIRE=7d

# CORS Configuration
CORS_ORIGIN=http://localhost:5173
```

### MongoDB Setup

1. **Install MongoDB** on your system
2. **Start MongoDB service**
3. **Create a database** named `blogspace`
4. **Update the MONGODB_URI** in your `.env` file

## 🎯 Usage

### Development Mode

Start both frontend and backend in development mode:

```bash
npm run dev
```

This will start:
- **Backend**: Express server with nodemon (port 5000)
- **Frontend**: Vite development server (port 5173)

### Production Mode

Build and start in production mode:

```bash
npm run build
npm run start
```

### Individual Services

Start only the backend:
```bash
npm run backend
```

Start only the frontend:
```bash
npm run frontend
```

## 📚 API Documentation

### Authentication Endpoints

- `POST /api/auth/register` - Register a new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user profile

### Blog Endpoints

- `GET /api/blogs` - Get all blogs
- `POST /api/blogs` - Create a new blog
- `GET /api/blogs/:id` - Get a specific blog
- `PUT /api/blogs/:id` - Update a blog
- `DELETE /api/blogs/:id` - Delete a blog

### File Endpoints

- `GET /api/files` - Get all files
- `POST /api/files` - Upload a new file
- `DELETE /api/files/:id` - Delete a file

## 🛠️ Development

### Available Scripts

From the root directory:

| Script | Description |
|--------|-------------|
| `npm run dev` | Start both frontend and backend in development mode |
| `npm run start` | Start both frontend and backend in production mode |
| `npm run install:all` | Install dependencies for all projects |
| `npm run build` | Build the frontend for production |
| `npm run backend` | Start only the backend development server |
| `npm run frontend` | Start only the frontend development server |

### Backend Scripts (from `/backend` directory)

| Script | Description |
|--------|-------------|
| `npm run dev` | Start development server with nodemon |
| `npm start` | Start production server |

### Frontend Scripts (from `/frontend` directory)

| Script | Description |
|--------|-------------|
| `npm run dev` | Start Vite development server |
| `npm run build` | Build for production |
| `npm run preview` | Preview production build |

### Development Workflow

1. **Install dependencies**: `npm run install:all`
2. **Set up environment variables** in `backend/.env`
3. **Start development servers**: `npm run dev`
4. **Open browser** to `http://localhost:5173`
5. **Make changes** - both servers will auto-reload

## 🚀 Deployment

### Frontend Deployment (Vercel/Netlify)

1. **Build the frontend**:
   ```bash
   cd frontend
   npm run build
   ```

2. **Deploy the `dist` folder** to your hosting platform

### Backend Deployment (Heroku/Railway)

1. **Set environment variables** in your hosting platform
2. **Deploy the `backend` folder**
3. **Update frontend API base URL** to point to your deployed backend

### Environment Variables for Production

```env
PORT=5000
NODE_ENV=production
MONGODB_URI=your_production_mongodb_uri
JWT_SECRET=your_production_jwt_secret
CORS_ORIGIN=https://your-frontend-domain.com
```

## 🤝 Contributing

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Commit your changes**: `git commit -m 'Add amazing feature'`
4. **Push to the branch**: `git push origin feature/amazing-feature`
5. **Open a Pull Request**

### Development Guidelines

- Follow the existing code style
- Add tests for new features
- Update documentation as needed
- Ensure all tests pass before submitting

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [React](https://reactjs.org/) - UI library
- [Express.js](https://expressjs.com/) - Web framework
- [MongoDB](https://www.mongodb.com/) - Database
- [Tailwind CSS](https://tailwindcss.com/) - Styling framework
- [Vite](https://vitejs.dev/) - Build tool

---

**Made with ❤️ by [Rishant](https://github.com/Rishant12220055)**

For questions or support, please open an [issue](https://github.com/Rishant12220055/Blog_Website/issues) on GitHub.