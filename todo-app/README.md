# 📋 RVCE Todo App — DevOps Lab Manual

This manual contains the installation commands for all required software, followed by the minimal execution commands for DevOps Experiments 1–9 (excluding 6).

---

## 💻 Part 1: Software Installation Commands

Run these commands on the laboratory system to install the required stack (Ubuntu/Debian environment):

### 1. Git Installation
```bash
sudo apt update
sudo apt install -y git
git --version
```

### 2. Node.js (v20 LTS) & npm Installation
```bash
sudo apt install -y curl
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
node --version
npm --version
```

### 3. Docker Engine Installation
```bash
sudo apt update
sudo apt install -y ca-certificates curl gnupg lsb-release
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo systemctl enable docker
sudo systemctl start docker
```

### 4. Jenkins Installation (using LTS repositories)
```bash
sudo apt install -y openjdk-17-jre
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install -y jenkins
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

### 5. Ngrok Installation (for local webhook testing)
```bash
curl -s https://ngrok-agent.s3.amazonaws.com/files/gated/g3-luc/ngrok.asc | sudo tee /etc/apt/trusted.gpg.d/ngrok.asc >/dev/null
echo "deb https://ngrok-agent.s3.amazonaws.com/files/gated/g3-luc/ default main" | sudo tee /etc/apt/sources.list.d/ngrok.list
sudo apt update
sudo apt install ngrok
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

1. Go to Jenkins UI: `http://localhost:8080`
2. Create **New Item** -> Name: `rvce-todo-app` -> Select **Pipeline**.
3. Under **Pipeline SCM**:
   - SCM: **Git**
   - Repository URL: `https://github.com/Dheeraj-02NK/CNA-Lab-Application.git`
   - Branch: `*/main`
   - Script Path: `todo-app/Jenkinsfile`
4. Click **Save** -> **Build Now**.

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
