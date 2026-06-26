# 📋 RVCE Todo App — DevOps Lab Manual

This manual contains the instructions to run all required services (Jenkins, Ngrok, etc.) via Docker, followed by the execution commands for DevOps Experiments 1–9 (excluding 6).

---

## 💻 Part 1: Service Configuration (Docker & Docker Compose)

Since Git, Node.js, and Docker are already installed on the laboratory systems, you can spin up Jenkins and Ngrok directly as Docker containers to avoid installation privileges.

### 1. Start Jenkins LTS Container
Run this command from the `todo-app` folder:
```bash
docker compose -f docker-compose.devops.yml up -d
```
- **Jenkins Access:** http://localhost:8080
- **Admin Password Retrieval:**
  ```bash
  docker logs jenkins-lab
  ```

### 2. Start Ngrok Container
```bash
# Add your authtoken and run
docker run -d --name ngrok-agent --net=host -e NGROK_AUTHTOKEN=<YOUR_NGROK_AUTHTOKEN> ngrok/ngrok http 8080
```

---

## 🧪 Part 2: Experiment Manual & Minimal Execution

### Project Setup
```bash
# Clone and enter project folder
git clone https://github.com/Dheeraj-02NK/CNA-Lab-Application.git
cd CNA-Lab-Application/todo-app

# Setup local configurations
cp .env.example server/.env
cp .env.example client/.env

# Install project dependencies
npm install
```

---

### Experiment 1: Version Control with Git

```bash
# 1. Initialize local repository
git init

# 2. Stage all modifications
git add .

# 3. Commit staged updates to local timeline
git commit -m "feat: setup CNA laboratory todo application"

# 4. View local commits list
git log --oneline
```

---

### Experiment 2: Collaborative Development with GitHub

```bash
# 1. Set default branch to main
git branch -M main

# 2. Add remote origin mapping
git remote add origin https://github.com/Dheeraj-02NK/CNA-Lab-Application.git

# 3. Push local changes to GitHub
git push -u origin main

# 4. Pull changes from remote
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

1. Start Jenkins container: `docker compose -f docker-compose.devops.yml up -d`
2. Go to Jenkins UI: `http://localhost:8080`.
3. Create **New Item** -> Name: `rvce-todo-app` -> Select **Pipeline**.
4. Under **Pipeline SCM**:
   - SCM: **Git**
   - Repository URL: `https://github.com/Dheeraj-02NK/CNA-Lab-Application.git`
   - Branch: `*/main`
   - Script Path: `todo-app/Jenkinsfile`
5. Click **Save** -> **Build Now**.

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

1. Start Ngrok container:
   ```bash
   docker run -d --name ngrok-agent --net=host -e NGROK_AUTHTOKEN=<YOUR_NGROK_AUTHTOKEN> ngrok/ngrok http 8080
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
