# 📋 RVCE Todo Application

A modern, production-quality **To-Do Application** built with **React.js** and **Node.js + Express.js**, designed specifically for **CNA Lab DevOps demonstrations** at RV College of Engineering.

![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Express.js](https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)
![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)

---

## 📖 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Technologies Used](#-technologies-used)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Running Locally](#-running-locally)
- [API Endpoints](#-api-endpoints)
- [Docker Commands](#-docker-commands)
- [Jenkins Pipeline](#-jenkins-pipeline)
- [Azure Deployment](#-azure-deployment)
- [GitHub Webhooks](#-github-webhooks)
- [Environment Variables](#-environment-variables)
- [Login Credentials](#-login-credentials)
- [Future Enhancements](#-future-enhancements)
- [License](#-license)

---

## 🌟 Overview

This is a full-stack To-Do application with a premium, modern UI inspired by **Notion**, **Linear**, and **Microsoft Fluent Design**. It uses **localStorage** for per-student task storage and a lightweight Express backend for authentication only.

The project is structured for seamless DevOps lab experiments:

- ✅ **Git & GitHub** — Version control and collaboration
- ✅ **Docker** — Containerization with multi-stage builds
- ✅ **Docker Compose** — Single-command deployment
- ✅ **Jenkins** — CI/CD pipeline automation
- ✅ **Azure App Service** — Cloud deployment from GitHub
- ✅ **Webhooks** — Automated build triggers

---

## ✨ Features

### 🔐 Authentication
- Simple login with hardcoded RVCE student credentials
- No database, JWT, or OAuth — clean and beginner-friendly

### 📊 Premium Dashboard
- Personalized welcome with student name
- Live date and time display
- Time-based greeting (Good Morning/Afternoon/Evening)
- Stats cards: Total, Completed, Pending, High Priority
- Animated progress bar with percentage

### ✅ Task Management
- **Create** tasks with title, description, priority, and due date
- **Edit** existing tasks
- **Delete** tasks
- **Complete** / **Undo** completion
- **Search** tasks in real-time
- **Filter** by status (All / Pending / Completed)
- Tasks sorted by newest first

### 🎨 UI/UX
- Glassmorphism design
- Smooth animations and transitions
- Dark mode toggle with localStorage persistence
- Responsive layout (desktop, tablet, mobile)
- Floating Action Button (FAB)
- Toast notifications
- Sidebar navigation
- Profile card with initials avatar

---

## 🛠️ Technologies Used

| Layer       | Technology           | Purpose                          |
|-------------|----------------------|----------------------------------|
| Frontend    | React.js (Vite)      | UI framework                     |
| Routing     | React Router         | Client-side navigation           |
| HTTP Client | Axios                | API requests                     |
| Icons       | Lucide React         | Modern icon library              |
| Toasts      | React Hot Toast      | Notification system              |
| Backend     | Node.js + Express    | API server                       |
| Storage     | localStorage         | Per-user task persistence        |
| Styling     | Vanilla CSS          | Custom design system             |
| DevOps      | Docker, Jenkins      | CI/CD and containerization       |

---

## 📁 Project Structure

```
rvce-todo-app/
├── client/                       # React Frontend (Vite)
│   ├── src/
│   │   ├── components/           # Reusable UI components
│   │   │   ├── LoadingScreen.jsx  # Loading spinner
│   │   │   ├── Sidebar.jsx        # Navigation sidebar
│   │   │   ├── TaskCard.jsx       # Individual task card
│   │   │   └── TaskModal.jsx      # Add/edit task modal
│   │   ├── context/              # React Context providers
│   │   │   ├── AuthContext.jsx    # Authentication state
│   │   │   └── ThemeContext.jsx   # Dark mode state
│   │   ├── pages/                # Route pages
│   │   │   ├── Login.jsx          # Login page
│   │   │   └── Dashboard.jsx      # Main dashboard
│   │   ├── utils/                # Helper modules
│   │   │   ├── api.js             # Axios API client
│   │   │   └── todoStorage.js     # localStorage CRUD
│   │   ├── App.jsx               # Root component with routing
│   │   ├── main.jsx              # Entry point
│   │   └── index.css             # Global design system
│   ├── index.html
│   ├── vite.config.js
│   └── package.json
├── server/                       # Express Backend
│   ├── server.js                 # API server + static file serving
│   ├── users.js                  # Hardcoded student data
│   └── package.json
├── Dockerfile                    # Multi-stage Docker build
├── docker-compose.yml            # Docker Compose configuration
├── Jenkinsfile                   # CI/CD pipeline definition
├── .env.example                  # Sample environment variables
├── .gitignore                    # Git ignore rules
├── LICENSE                       # MIT License
├── README.md                     # This file
└── package.json                  # Root project configuration
```

---

## 🚀 Installation

### Prerequisites

- **Node.js** 18 or higher
- **npm** (comes with Node.js)

### Steps

```bash
# 1. Clone the repository
git clone <your-github-repo-url>
cd rvce-todo-app

# 2. Copy environment file
cp .env.example server/.env

# 3. Install all dependencies (server + client)
npm run install:all
```

---

## 🏃 Running Locally

### Development Mode (Hot Reload)

```bash
# Start both frontend and backend concurrently
npm run dev
```

| Service  | URL                        |
|----------|----------------------------|
| Frontend | http://localhost:5173       |
| Backend  | http://localhost:3000       |
| Health   | http://localhost:3000/api/health |

### Production Mode

```bash
# Build the frontend
npm run build

# Start the production server
npm start
```

The full application runs on **http://localhost:3000**

---

## 🔗 API Endpoints

| Method | Endpoint       | Description              |
|--------|----------------|--------------------------|
| GET    | `/api/health`  | Server health check      |
| POST   | `/api/login`   | Student authentication   |

### `GET /api/health`

```json
{
  "status": "Running",
  "application": "RVCE Todo App",
  "version": "1.0.0",
  "timestamp": "2025-06-26T15:00:00.000Z",
  "uptime": 123.45,
  "environment": "production"
}
```

### `POST /api/login`

**Request:**
```json
{
  "rvceId": "RVCE25MIT015",
  "password": "1234"
}
```

**Success Response:**
```json
{
  "success": true,
  "name": "DHEERAJ N KASHYAP",
  "rvceId": "RVCE25MIT015"
}
```

**Error Response:**
```json
{
  "success": false,
  "message": "Invalid RVCE ID or Password."
}
```

---

## 🐳 Docker Commands

### Build and Run

```bash
# Build the Docker image
docker build -t todo-app .

# Run the container
docker run -p 3000:3000 todo-app
```

### Using Docker Compose

```bash
# Start in background
docker compose up -d

# View logs
docker compose logs -f

# Stop
docker compose down

# Rebuild and start
docker compose up --build -d
```

Access the app at **http://localhost:3000**

### Useful Docker Commands

```bash
# List running containers
docker ps

# Check container health
docker inspect --format='{{.State.Health.Status}}' rvce-todo-app

# Enter the container shell
docker exec -it rvce-todo-app sh

# Remove all stopped containers
docker container prune
```

---

## 🔧 Jenkins Pipeline

### Setup Steps

1. Open Jenkins Dashboard → **New Item**
2. Enter name: `rvce-todo-app` → Select **Pipeline** → Click **OK**
3. Under **Pipeline**:
   - Definition: **Pipeline script from SCM**
   - SCM: **Git**
   - Repository URL: `<your-github-repo-url>`
   - Branch: `*/main`
   - Script Path: `Jenkinsfile`
4. Click **Save** → **Build Now**

### Pipeline Stages

| Stage                  | Description                                |
|------------------------|--------------------------------------------|
| Checkout               | Pulls code from GitHub                     |
| Install Dependencies   | Runs `npm install` for server and client   |
| Build Application      | Builds React frontend for production       |
| Verify Build           | Checks that `client/dist/index.html` exists|
| Docker Build           | Builds Docker image (if Docker is available)|
| Pipeline Complete      | Prints success summary                     |

---

## ☁️ Azure Deployment

### Deploy from GitHub (Recommended)

1. Create an **Azure App Service** (Web App)
   - Runtime: **Node 20 LTS**
   - OS: **Linux**
2. Go to **Deployment Center**
3. Source: **GitHub**
4. Select your repository and branch
5. Azure will auto-detect the `package.json` and deploy

### Azure Configuration

Set these **Application Settings** in Azure:

| Setting     | Value        |
|-------------|--------------|
| `PORT`      | `3000`       |
| `NODE_ENV`  | `production` |

### Startup Command

```bash
npm run build && npm start
```

### Verify Deployment

Visit: `https://<your-app-name>.azurewebsites.net/api/health`

---

## 🔔 GitHub Webhooks

### For Jenkins Auto-Build

1. Go to your GitHub repo → **Settings** → **Webhooks**
2. Click **Add webhook**
3. Payload URL: `http://<jenkins-url>/github-webhook/`
4. Content type: `application/json`
5. Events: **Just the push event**
6. Click **Add webhook**

Now every `git push` will automatically trigger a Jenkins build!

---

## ⚙️ Environment Variables

| Variable   | Default       | Description              |
|------------|---------------|--------------------------|
| `PORT`     | `3000`        | Server port              |
| `NODE_ENV` | `development` | Environment mode         |

Copy the example file:

```bash
cp .env.example server/.env
```

---

## 🔑 Login Credentials

**Password for all students:** `1234`

### MIT Students

| Name                              | RVCE ID        |
|-----------------------------------|----------------|
| RAHUL K                           | RVCE25MIT001   |
| DEEPAK M                          | RVCE25MIT002   |
| VISMAYA R                         | RVCE25MIT003   |
| LIKHITH RAJ A                     | RVCE25MIT004   |
| SHREYAS S                         | RVCE25MIT005   |
| AMULYA M D                        | RVCE25MIT006   |
| VINAYAK U MALAWAD                 | RVCE25MIT007   |
| BHARATH SHIVAKUMAR BANAKAR        | RVCE25MIT008   |
| HARSHAN N                         | RVCE25MIT009   |
| K S DARSHAN                       | RVCE25MIT010   |
| S JANVI                           | RVCE25MIT011   |
| SHUBHAM HUNDALEKAR                | RVCE25MIT012   |
| S ABHINANDAN YADAV                | RVCE25MIT013   |
| MANOJ M U                         | RVCE25MIT014   |
| DHEERAJ N KASHYAP                 | RVCE25MIT015   |
| NITHIN G P                        | RVCE25MIT016   |
| HARSHITH H S                      | RVCE25MIT017   |
| SAGAR KUMAR                       | RVCE25MIT018   |

### MSE Students

| Name                                    | RVCE ID        |
|-----------------------------------------|----------------|
| IMPU D                                  | RVCE25MSE001   |
| SUJAI GOWDA J                           | RVCE25MSE002   |
| SUHAS V                                 | RVCE25MSE003   |
| NAYANA R A                              | RVCE25MSE004   |
| ANANYA R                                | RVCE25MSE005   |
| LAVANYA R                               | RVCE25MSE006   |
| M VISHAL PRANAV                         | RVCE25MSE007   |
| AVIKSHA NAYANA GOWDA                    | RVCE25MSE008   |
| K S SHARAN KUMAR                        | RVCE25MSE009   |
| SAHANA M R                              | RVCE25MSE010   |
| GAGANA B R                              | RVCE25MSE011   |
| THUMMAGUNTA VENKATA NAGA SRAVANI        | RVCE25MSE012   |
| PRATHAMESH RAVINDRANATH PATIL           | RVCE25MSE013   |
| SUVISHESH C                             | RVCE25MSE014   |
| POORNIMA B                              | RVCE25MSE015   |
| CHIRAG M G                              | RVCE25MSE016   |
| SACHIN B S                              | RVCE25MSE017   |
| PRAJWAL M D                             | RVCE25MSE018   |

---

## 🚀 Future Enhancements

- [ ] Task categories and labels
- [ ] Due date reminders
- [ ] Drag-and-drop task reordering
- [ ] Export tasks to CSV/PDF
- [ ] Multiple todo lists per user
- [ ] Collaborative shared tasks
- [ ] Push notifications
- [ ] PWA support for offline access

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

**Built with ❤️ for RV College of Engineering — CNA Lab 2025**
