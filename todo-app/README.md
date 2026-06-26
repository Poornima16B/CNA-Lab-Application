# 📋 RVCE Todo App — DevOps Lab Manual

A streamlined guide for executing DevOps Experiments 1–9 (excluding 6).

---

## 🛠️ Project Setup & Local Execution

### Prerequisites
- Node.js (v20+)
- Git
- Docker & Docker Compose
- Jenkins
- Azure CLI

### Installation
```bash
# Clone the repository
git clone https://github.com/Dheeraj-02NK/CNA-Lab-Application.git
cd CNA-Lab-Application/todo-app

# Copy environment variables
cp .env.example server/.env
cp .env.example client/.env

# Install all dependencies (Root, Client, and Server)
npm install
```

### Running Locally (Development Mode)
```bash
npm run dev
```
- **Frontend URL:** http://localhost:5173
- **Backend URL:** http://localhost:3000
- **Credentials:** RVCE ID (e.g., `RVCE25MIT015`) / Password: `1234`

---

## 🧪 Experiments

### Experiment 1: Version Control with Git

**Objective:** Initialize Git locally, track and stage changes, commit snapshots, and view revision history.

```bash
# 1. Initialize local repository
git init

# 2. Configure developer identity
git config --local user.name "Dheeraj N Kashyap"
git config --local user.email "dheeraj.mit@rvce.edu.in"

# 3. Check status of files
git status

# 4. Stage all modified and untracked files
git add .

# 5. Commit staged files
git commit -m "feat: initial commit of RVCE Todo App and DevOps configurations"

# 6. Review revision history
git log --oneline
```

---

### Experiment 2: Collaborative Development with GitHub

**Objective:** Map local repository to remote origin, push code, and clone existing remote repositories.

```bash
# 1. Set main branch as the default branch
git branch -M main

# 2. Add remote origin mapping
git remote add origin https://github.com/Dheeraj-02NK/CNA-Lab-Application.git

# 3. Push local changes to remote main branch
git push -u origin main

# 4. Clone repository into a test directory to verify
git clone https://github.com/Dheeraj-02NK/CNA-Lab-Application.git /tmp/test-clone
```

---

### Experiment 3: Containerization with Docker & Docker Compose

**Objective:** Containerize the React + Node.js application using a multi-stage `Dockerfile` and manage execution via `docker-compose.yml`.

```bash
# 1. Build the production Docker image
docker build -t rvce-todo-app:1.0.0 .

# 2. List built images to verify
docker images | grep rvce-todo-app

# 3. Run the container in detached mode on port 3000
docker run -d -p 3000:3000 --name todo-container rvce-todo-app:1.0.0

# 4. Verify running container and map port
docker ps

# 5. Test health status API endpoint
curl http://localhost:3000/api/health

# 6. Stop and remove the running container
docker stop todo-container
docker rm todo-container

# 7. Start environment using Docker Compose
docker compose up -d

# 8. Stop environment using Docker Compose
docker compose down
```

---

### Experiment 4: CI/CD Pipeline Automation with Jenkins

**Objective:** Configure a Jenkins declarative pipeline utilizing the SCM workflow and `Jenkinsfile`.

1. **Start Jenkins:**
   ```bash
   docker run -d -p 8080:8080 -p 50000:50000 --name jenkins -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
   ```
2. Retrieve initial admin password using `docker logs jenkins`.
3. Open Jenkins at `http://localhost:8080` and install default plugins.
4. Create a **New Item** named `rvce-todo-app` of type **Pipeline**.
5. Under **Pipeline Definition**, select **Pipeline script from SCM**.
6. Set SCM to **Git**, paste Repository URL `https://github.com/Dheeraj-02NK/CNA-Lab-Application.git`.
7. Set Branch specifier to `*/main`.
8. Set Script Path to `todo-app/Jenkinsfile` and click **Save**.
9. Click **Build Now** to execute and observe the stages under **Console Output**.

---

### Experiment 5: Cloud Deployment on Azure App Service

**Objective:** Configure Azure App Service Web App with GitHub Integration (Continuous Deployment).

1. Log in to the [Azure Portal](https://portal.azure.com).
2. Create a **Web App** (Code, Node 20 LTS runtime, Linux OS).
3. Navigate to **Deployment Center** within the created Web App resource.
4. Select **GitHub** as the source provider, authorize your account, and choose your repository `CNA-Lab-Application` and branch `main`.
5. Under Web App **Configuration** -> **Application Settings**, add:
   - Name: `PORT`, Value: `3000`
6. Set the Web App **Startup Command** under General Settings:
   ```bash
   npm run build && npm start
   ```
7. Click **Save** and wait for the GitHub Actions run to complete. Verify at:
   `https://<your-web-app-name>.azurewebsites.net/api/health`

---

### Experiment 6: (Intentionally Omitted)
*Experiment 6 is an internal laboratory test assessment and is omitted from the manual.*

---

### Experiment 7: DevOps Foundational Lifecycle & Workflow

**Objective:** Run the multi-stage delivery lifecycle steps manually on a workspace.

```bash
# 1. Clean workspace environment
rm -rf node_modules client/node_modules server/node_modules client/dist

# 2. Code phase: Install dependency packages
npm run install:all

# 3. Build phase: Compile React production code
npm run build

# 4. Release & Run phase: Start Express production server
npm start
```

---

### Experiment 8: DevSecOps (Dependency Scanning)

**Objective:** Implement Shift-Left security by running automated vulnerability scans on dependencies.

```bash
# Scan Express backend dependencies for vulnerabilities
cd server && npm audit

# Scan React frontend dependencies for vulnerabilities
cd ../client && npm audit
```

---

### Experiment 9: GitHub Webhooks for Automated Jenkins Triggering

**Objective:** Connect GitHub pushing events to automatically trigger Jenkins builds.

1. Expose the local Jenkins instance (port 8080) to the internet:
   ```bash
   ngrok http 8080
   ```
   Copy the generated HTTPS URL (e.g., `https://xxxx-xx-xx-xx.ngrok-free.app`).
2. Go to your GitHub repository -> **Settings** -> **Webhooks** -> **Add Webhook**.
3. Set Payload URL to: `https://<your-ngrok-url>/github-webhook/`
4. Set Content Type to `application/json`. Click **Add Webhook**.
5. In your Jenkins job settings, check **GitHub hook trigger for GITScm polling** under Build Triggers and save.
6. Commit a small change and push:
   ```bash
   git commit --allow-empty -m "trigger: webhooks test"
   git push origin main
   ```
7. Verify that Jenkins triggers a new build execution automatically.

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
