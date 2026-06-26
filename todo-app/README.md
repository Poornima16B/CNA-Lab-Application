# 📋 RVCE Todo App — DevOps Lab Manual

This manual contains setup steps to run the application and Jenkins using a single Docker Compose command, followed by execution commands for DevOps Experiments 1–9 (excluding 6).

---

## 💻 Part 1: Service Configurations (Docker & Docker Compose)

You can launch both the **Todo Application** and **Jenkins CI/CD Server** simultaneously using Docker Compose.

### 1. Launch Services
Run this command from the `todo-app` folder:
```bash
docker compose up -d
```

| Service | Access URL |
|---|---|
| **Todo App** | http://localhost:3000 |
| **Jenkins GUI** | http://localhost:8080 |

### 2. Stop Services
```bash
docker compose down
```

---

## ⚙️ Part 2: Jenkins GUI Setup Guide

Follow these steps to configure Jenkins through the web interface after running `docker compose up -d`:

### 1. Retrieve Administrator Password
To unlock the Jenkins UI, read the secret token generated during startup:
```bash
docker logs jenkins-lab
```
*(Copy the 32-character alphanumeric code printed in the logs).*

### 2. Unlock Jenkins
1. Open **http://localhost:8080** in your browser.
2. Paste the copied administrator password into the **Administrator password** field.
3. Click **Continue**.

### 4. Create Admin Account
1. On the customization page, click **Install suggested plugins**.
2. Create your admin profile once installation finishes.

---

## 🧪 Part 3: Experiment Manual & Minimal Execution

### Project Setup
To begin the lab, clone the project and configure dependencies:
```bash
# 1. Clone repository
git clone https://github.com/Dheeraj-02NK/CNA-Lab-Application.git

# 2. Go to project directory
cd CNA-Lab-Application/todo-app

# 3. Setup configuration files
cp .env.example server/.env
cp .env.example client/.env

# 4. Install all server and client dependencies
npm install
```

---

### Experiment 1: Version Control with Git

> 💡 **Note for Students:** Since you cloned this project from GitHub, it is already a Git repository. To practice `git init` from scratch for this experiment, delete the existing configuration folder:
> ```bash
> rm -rf .git
> ```

```bash
# 1. Initialize local repository
git init

# 2. Configure developer identity
git config --local user.name "Your Name"
git config --local user.email "Your Email"

# 3. Check status of untracked files
git status

# 4. Stage all files for commit
git add .

# 5. Commit the files to local history
git commit -m "feat: initial commit of RVCE Todo App"

# 6. View the commit log
git log --oneline
```

---

### Experiment 2: Collaborative Development with GitHub

> 💡 **Note for Students:** Replace the URL below with your own personal GitHub repository URL.

```bash
# 1. Create main branch
git branch -M main

# 2. Add remote origin link
git remote add origin https://github.com/<your-github-username>/CNA-Lab-Application.git

# 3. Push local changes to your remote repository
git push -u origin main

# 4. Pull changes from remote to verify sync
git pull origin main
```

---

### Experiment 3: Containerization with Docker & Docker Compose

```bash
# 1. Build Docker container image
docker build -t rvce-todo-app:1.0.0 .

# 2. Run container in background on port 3000
docker run -d -p 3000:3000 --name todo-container rvce-todo-app:1.0.0

# 3. Stop and remove container
docker stop todo-container && docker rm todo-container

# 4. Start using Docker Compose
docker compose up -d

# 5. Stop using Docker Compose
docker compose down
```

---

### Experiment 4: CI/CD Pipeline Automation with Jenkins

1. Go to Jenkins UI: **http://localhost:8080**
2. Click **New Item** -> Name: `rvce-todo-app` -> Select **Pipeline** -> Click **OK**.
3. Scroll to **Pipeline** section and select:
   - Definition: **Pipeline script from SCM**
   - SCM: **Git**
   - Repository URL: `https://github.com/Dheeraj-02NK/CNA-Lab-Application.git`
   - Branch Specifier: `*/main`
   - Script Path: `todo-app/Jenkinsfile`
4. Click **Save**.
5. Click **Build Now** in the left menu, then click the build number to view progress under **Console Output**.

---

### Experiment 5: Cloud Deployment on Azure App Service

1. Log in to [Azure Portal](https://portal.azure.com).
2. Create a Linux **Web App** with Runtime Stack **Node 20 LTS**.
3. Under **Deployment Center**:
   - Source: **GitHub**
   - Repository: `CNA-Lab-Application`, Branch: `main`
4. In Web App **Configuration** -> Add Application Setting:
   - Name: `PORT`, Value: `3000`
5. Under General Settings set **Startup Command**:
   ```bash
   npm run build && npm start
   ```

---

### Experiment 6: (Intentionally Omitted)
*Assessment evaluation test stage. Omitted.*

---

### Experiment 7: DevOps Foundational Lifecycle & Workflow

```bash
# 1. Clear previous outputs
rm -rf node_modules client/node_modules server/node_modules client/dist

# 2. Run build installation script
npm run install:all

# 3. Compile client code for distribution
npm run build

# 4. Run Express production server
npm start
```

---

### Experiment 8: DevSecOps (Dependency Scanning)

```bash
# Scan Express backend dependencies for vulnerabilities
cd server && npm audit

# Scan React frontend dependencies for vulnerabilities
cd ../client && npm audit
```

---

### Experiment 9: GitHub Webhooks for Automated Jenkins Triggering

1. Start Ngrok tunnel on your local machine:
   ```bash
   ngrok http 8080
   ```
2. Go to GitHub repo -> **Settings** -> **Webhooks** -> **Add Webhook**.
3. Set Payload URL to: `https://<ngrok-url-subdomain>/github-webhook/`
4. Set Content Type to `application/json` -> Click **Add Webhook**.
5. Enable **GitHub hook trigger for GITScm polling** in Jenkins job settings.
6. Push a commit to test automated execution:
   ```bash
   git commit --allow-empty -m "trigger: webhooks execution verification"
   git push origin main
   ```

---

## 🔌 API Specifications

### Health Check
- **Endpoint:** `GET /api/health`
- **Output:**
  ```json
  {
    "status": "Running",
    "application": "RVCE Todo App",
    "version": "1.0.0"
  }
  ```

### Authentication
- **Endpoint:** `POST /api/login`
- **Body:**
  ```json
  {
    "rvceId": "RVCE25MIT015",
    "password": "1234"
  }
  ```
- **Output:**
  ```json
  {
    "success": true,
    "name": "DHEERAJ N KASHYAP",
    "rvceId": "RVCE25MIT015"
  }
  ```
