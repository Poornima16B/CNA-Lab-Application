# 📋 RVCE Todo App — DevOps Lab Manual (Webhook Test 2)

This manual contains the absolute minimal commands required to execute DevOps Experiments 1–9 (excluding 6).

---

## 🚀 Step 1: Initial Git Clone & Project Setup

Execute these commands to pull the repository and install all dependencies:

```bash
# 1. Clone the repository
git clone https://github.com/Dheeraj-02NK/CNA-Lab-Application.git

# 2. Go to the project folder
cd CNA-Lab-Application

# 3. Setup configurations (Linux / macOS)
cp .env.example server/.env
cp .env.example client/.env

# 3. Setup configurations (Windows)
copy .env.example server\.env
copy .env.example client\.env

# 4. Install all dependencies (server + client)
npm install
```

---

## 💻 Step 2: Multi-Platform Software Installation

If Git, Node, Docker, Jenkins, or Ngrok are missing, install them using these commands:

### 1. Git
* **Linux:** `sudo apt update && sudo apt install -y git`
* **macOS:** `brew install git`
* **Windows:** `winget install --id Git.Git -e --source winget`

### 2. Node.js (v20 LTS) & npm
* **Linux:** `curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash - && sudo apt install -y nodejs`
* **macOS:** `brew install node@20 && brew link node@20`
* **Windows:** `winget install -e --id OpenJS.NodeJS.LTS`

### 3. Docker & Docker Compose
* **Linux:**
  ```bash
  sudo apt update && sudo apt install -y ca-certificates curl gnupg lsb-release
  sudo mkdir -p /etc/apt/keyrings
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
  echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  sudo apt update && sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
  sudo systemctl enable docker && sudo systemctl start docker
  ```
* **macOS:** `brew install --cask docker`
* **Windows:** `winget install -e --id Docker.DockerDesktop`

### 4. Jenkins
* **Linux:**
  ```bash
  sudo apt update && sudo apt install -y openjdk-21-jre openjdk-21-jdk
  sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 5BA31D57EF5975CA 7198F4B714ABFC68
  echo "deb https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
  sudo apt update && sudo apt install -y jenkins
  sudo systemctl enable jenkins && sudo systemctl start jenkins
  ```
* **macOS:** `brew install jenkins-lts && brew services start jenkins-lts`
* **Windows:** `winget install -e --id Jenkins.Jenkins`

### 5. Ngrok
* **Linux:**
  ```bash
  curl -s https://ngrok-agent.s3.amazonaws.com/files/gated/g3-luc/ngrok.asc | sudo tee /etc/apt/trusted.gpg.d/ngrok.asc >/dev/null
  echo "deb https://ngrok-agent.s3.amazonaws.com/files/gated/g3-luc/ default main" | sudo tee /etc/apt/sources.list.d/ngrok.list
  sudo apt update && sudo apt install ngrok
  ```
* **macOS:** `brew install ngrok/ngrok/ngrok`
* **Windows:** `winget install -e --id ngrok.ngrok`

---

## ⚙️ Step 3: Run Jenkins & Todo App via Docker Compose

Start both services simultaneously:
```bash
# Launch services in background
docker compose up -d
```
* **Todo App URL:** http://localhost:3000
* **Jenkins GUI URL:** http://localhost:8080

**To unlock Jenkins:**
1. Fetch admin password: `docker logs jenkins-lab`
2. Open http://localhost:8080, paste password, and click **Install suggested plugins**.

**To stop services:**
```bash
docker compose down
```

---

## 🧪 Step 4: DevOps Experiments Manual

### Experiment 1: Version Control with Git
*(Delete cloned `.git` to practice initialization from scratch)*
```bash
# 1. Clear cloned Git metadata (Linux / macOS)
rm -rf .git

# 1. Clear cloned Git metadata (Windows)
rmdir /s /q .git

# 2. Initialize new Git repository
git init

# 3. Setup local name and email
git config --local user.name "Your Name"
git config --local user.email "Your Email"

# 4. Stage and commit files
git add .
git commit -m "feat: initial commit"

# 5. View git logs
git log --oneline
```

---

### Experiment 2: Collaborative Development with GitHub
```bash
# 1. Rename default branch
git branch -M main

# 2. Map local repository to your remote GitHub profile
git remote add origin https://github.com/<your-github-username>/CNA-Lab-Application.git

# 3. Push code upstream
git push -u origin main

# 4. Pull updates
git pull origin main
```

---

### Experiment 3: Containerization with Docker & Docker Compose
```bash
# 1. Build Docker image
docker build -t rvce-todo-app:1.0.0 .

# 2. Run container in background on port 3000
docker run -d -p 3000:3000 --name todo-container rvce-todo-app:1.0.0

# 3. Stop and delete container
docker stop todo-container
docker rm todo-container

# 4. Run using Docker Compose
docker compose up -d

# 5. Stop Compose environment
docker compose down
```

---

### Experiment 4: CI/CD Pipeline Automation with Jenkins

**Procedure**
1. Open Jenkins: `http://localhost:8080`
2. Click **New Item**.
3. Enter a project name (Example: `CNA Lab Apps`).
4. Select **Pipeline**.
5. Under Pipeline configuration:
   - Definition → **Pipeline script from SCM**
   - SCM → **Git**
   - Repository URL → `https://github.com/Dheeraj-02NK/CNA-Lab-Application.git`
   - Branch → `*/main`
   - Script Path → `Jenkinsfile`
6. Click **Save**.
7. Click **Build Now**.
8. Open **Console Output** to verify the laboratory demonstration pipeline.

---

### Experiment 5: Cloud Deployment on Azure App Service

**Procedure**
1. Open the [Azure Dashboard](https://portal.azure.com).
2. Create a new Virtual Machine (VM) to demonstrate cloud infrastructure provisioning.
3. Wait for the VM allocation to complete.
4. Delete the Virtual Machine (VM) to avoid unnecessary billing and demonstrate resource de-allocation.

---

### Experiment 6: (Intentionally Omitted)
*Assessment evaluation test stage. Omitted.*

---

### Experiment 7: DevOps Foundational Lifecycle & Workflow
*(Manual execution of stages)*
```bash
# 1. Clean workspace (Linux / macOS)
rm -rf node_modules client/node_modules server/node_modules client/dist

# 1. Clean workspace (Windows)
rmdir /s /q node_modules client\node_modules server\node_modules client\dist

# 2. Code phase: Install dependencies
npm run install:all

# 3. Build phase: Compile React project
npm run build

# 4. Release & Operate phase: Start server
npm start
```

---

### Experiment 8: DevSecOps (Dependency Scanning)
```bash
# Scan Express server packages
cd server
npm audit

# Scan React client packages
cd ../client
npm audit
```

---

### Experiment 9: GitHub Webhooks

**Procedure**

**Step 1**
1. Open [Svix Play](https://play.svix.com/).
2. Generate a new webhook endpoint.
3. Copy the generated Webhook URL.
   *Example:* `https://play.svix.com/in/e_xxxxxxxxxxxxxxxxxxxxxxxxx`
   *(Use your own generated URL)*

**Step 2**
1. Open your GitHub repository.
2. Navigate to: `Settings` → `Webhooks` → `Add Webhook`

**Step 3**
Configure the webhook:
* **Payload URL:** `<Paste your Svix Play Webhook URL>`
* **Content Type:** `application/json`
* **Secret:** *(Leave Empty)*
* **SSL Verification:** `Enable SSL Verification`
* **Events:** `Just the push event`
* Click **Add Webhook**.

**Step 4**
Make a small change to your repository.
```bash
git add .
git commit -m "Webhook Test"
git push origin main
```

**Step 5**
1. Return to Svix Play.
2. Refresh the page.
3. Observe the incoming webhook request to verify that GitHub has delivered the Push event successfully.

---

## 🚀 Step 5: Cloud Deployment (Experiments 10–18)

---

### Experiment 10: Prepare Repository for Cloud Deployment

Before deploying, ensure your repository structure is correct (files at the root level, not nested inside a subfolder).

```bash
# Verify your structure looks like this:
# CNA-Lab-Application/
# ├── client/       ← React frontend
# ├── server/       ← Node.js backend
# ├── Dockerfile
# ├── Jenkinsfile
# ├── docker-compose.yml
# └── README.md

git log --oneline -5
```

---

### Experiment 11: Deploy Backend API on Render

**Procedure**
1. Open [https://render.com](https://render.com) and sign in / create a free account.
2. Click **+ New** → **Web Service**.
3. Connect your GitHub account and select the `CNA-Lab-Application` repository.
4. Fill in the configuration fields:
   * **Name:** `CNA-Lab-Application`
   * **Language:** `Node`
   * **Branch:** `main`
   * **Root Directory:** `server`
   * **Build Command:** `npm install`
   * **Start Command:** `npm start`
   * **Instance Type:** `Free`
5. Click **Create Web Service**.
6. Wait 2–3 minutes for the build to complete.
7. Copy the URL shown at the top (e.g., `https://cna-lab-application.onrender.com`).

**Verify the backend is live:**
Open your browser and visit:
```
https://cna-lab-application.onrender.com/api/health
```
Expected response:
```json
{ "status": "Running", "application": "RVCE Todo App", "version": "1.0.0" }
```

---

### Experiment 12: Deploy Frontend on Netlify

**Procedure**
1. Open [https://netlify.com](https://netlify.com) and sign in / create a free account.
2. Click **Add new site** → **Import an existing project**.
3. Select **GitHub** as the Git provider and authorize Netlify.
4. Choose the `CNA-Lab-Application` repository.
5. Fill in the **Build settings**:
   * **Branch to deploy:** `main`
   * **Base directory:** `client`
   * **Build command:** `npm run build`
   * **Publish directory:** `client/dist`
   * **Functions directory:** *(leave empty)*
6. Expand **Environment variables** → Click **Add key/value pairs**:
   * **Key:** `VITE_API_URL`
   * **Value:** `https://cna-lab-application.onrender.com` *(your Render URL)*
7. Click **Deploy site**.
8. Wait 2–3 minutes for the build to complete.
9. Copy the Netlify URL (e.g., `https://cna-lab-todo.netlify.app`).

---

### Experiment 13: Verify Full Stack Application

Open your Netlify URL in the browser and verify the entire application works end-to-end.

**Login credentials:**
* **RVCE ID:** `RVCE25MIT015`
* **Password:** `1234`

**Checklist:**
- [ ] Login page loads on Netlify URL
- [ ] Sign In button connects to Render backend
- [ ] Dashboard loads after successful login
- [ ] Tasks can be created, edited, and deleted

---

### Experiment 14: Configure Continuous Deployment (Netlify)

Netlify automatically redeploys every time you push to GitHub. Verify this:

```bash
# Make a small change
echo "# Deploy test" >> README.md

# Push to GitHub
git add .
git commit -m "test: trigger netlify auto-deploy"
git push origin main
```

1. Go to your **Netlify Dashboard** → **Deploys**.
2. You will see a new deploy triggered automatically within seconds.
3. Wait for it to show **Published** status.

---

### Experiment 15: Configure Continuous Deployment (Render)

Render also auto-deploys on every push. Verify this:

1. After pushing in Experiment 14, go to your **Render Dashboard** → **Events**.
2. You will see a new deploy triggered automatically.
3. Wait for it to show **Live** status.

---

### Experiment 16: Environment Variables & Configuration Management

**Procedure — Update the backend API URL on Netlify:**
1. Go to **Netlify Dashboard** → **Site Configuration** → **Environment Variables**.
2. Click **Add a variable** or edit `VITE_API_URL`.
3. Change the value to a new URL (e.g., if you re-deploy your backend).
4. Go to **Deploys** → Click **Trigger deploy** → **Deploy site** to apply the new variable.

**Procedure — Add environment variables on Render:**
1. Go to **Render Dashboard** → **Environment**.
2. Click **Add Environment Variable**.
3. Add any required secrets (e.g., `NODE_ENV=production`).
4. Render automatically restarts the service when variables are saved.

---

### Experiment 17: Monitor Logs & Application Health

**Render (Backend) Logs:**
1. Go to **Render Dashboard** → **Logs**.
2. Observe real-time server logs.
3. Visit `https://<your-render-url>/api/health` to check the health endpoint.

**Netlify (Frontend) Logs:**
1. Go to **Netlify Dashboard** → **Deploys**.
2. Click on any deploy to view its **build log**.
3. Verify the build completed successfully with no errors.

---

### Experiment 18: Full DevOps Lifecycle Summary

This experiment demonstrates the complete DevOps pipeline from code to cloud.

| Stage | Tool | Action |
|-------|------|--------|
| **Plan** | GitHub Issues | Track features and bugs |
| **Code** | VS Code + Git | Write and commit code |
| **Build** | Netlify / Render | Auto-build on push |
| **Test** | npm audit | Scan for vulnerabilities |
| **Release** | GitHub | Tag a release version |
| **Deploy** | Netlify + Render | Auto-deploy to cloud |
| **Operate** | Render Dashboard | Monitor logs and uptime |
| **Monitor** | Health API | Verify service health |

**Final verification commands:**
```bash
# Check git history
git log --oneline

# Verify remote is connected
git remote -v

# Check all files are tracked
git status
```

---

## 🔌 API Specifications

### Health Check
`GET /api/health`
```json
{
  "status": "Running",
  "application": "RVCE Todo App",
  "version": "1.0.0"
}
```

### Authentication
`POST /api/login` (Body: `{"rvceId": "RVCE25MIT015", "password": "1234"}`)
```json
{
  "success": true,
  "name": "DHEERAJ N KASHYAP",
  "rvceId": "RVCE25MIT015"
}
```
