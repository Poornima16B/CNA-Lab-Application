# 📋 RVCE Todo Application & DevOps Lab Manual
### Department of Information Science & Engineering / Computer Science & Engineering
**RV College of Engineering®, Bengaluru - 560059**

* **Subject:** Computer Networks and Applications Laboratory / DevOps Lab
* **Semester:** 2nd Semester M.Tech (MIT / MSE)
* **Author:** DHEERAJ N KASHYAP (USN: RVCE25MIT015)
* **Academic Year:** 2025-2026

---

## 📖 Table of Contents
1. [Project Overview](#-1-project-overview)
2. [Folder Structure](#-2-folder-structure)
3. [Software Requirements](#-3-software-requirements)
4. [Installation & Setup](#-4-installation--setup)
5. [DevOps Experiment Guide](#-devops-experiment-guide)
   - [Experiment 1: Version Control with Git](#experiment-1-version-control-with-git)
   - [Experiment 2: Collaborative Development with GitHub](#experiment-2-collaborative-development-with-github)
   - [Experiment 3: Containerization with Docker & Docker Compose](#experiment-3-containerization-with-docker--docker-compose)
   - [Experiment 4: CI/CD Pipeline Automation with Jenkins](#experiment-4-cicd-pipeline-automation-with-jenkins)
   - [Experiment 5: Cloud Deployment on Azure App Service](#experiment-5-cloud-deployment-on-azure-app-service)
   - [Experiment 6: (Intentionally Omitted - Internal Lab Assessment)](#experiment-6-intentionally-omitted)
   - [Experiment 7: DevOps Foundational Lifecycle & Workflow](#experiment-7-devops-foundational-lifecycle--workflow)
   - [Experiment 8: DevSecOps (Shift-Left Security & Scanning)](#experiment-8-devsecops)
   - [Experiment 9: GitHub Webhooks for Automated Jenkins Triggering](#experiment-9-github-webhooks-for-automated-jenkins-triggering)
6. [API Documentation](#-6-api-documentation)
7. [Comprehensive Troubleshooting Manual (20+ Scenarios)](#-7-comprehensive-troubleshooting-manual)
8. [Frequently Asked Questions (30+ FAQs)](#-8-frequently-asked-questions)
9. [Top 50 Viva-Voce Questions & Answers](#-9-top-50-viva-voce-questions--answers)
10. [Future Enhancements & Project Scope](#-10-future-enhancements--project-scope)
11. [Conclusion](#-11-conclusion)

---

## 🚀 1. Project Overview

The **RVCE Todo Application** is a production-grade, containerized web application built on the **React-Node-Express** stack. It is custom-tailored to serve as a single, unified codebase for executing college DevOps laboratory experiments.

### Key Objectives
* **Database-Less Architecture:** The application operates without MongoDB, MySQL, or Postgres. Tasks are isolated using browser-level `localStorage` mapped to individual RVCE Student IDs (e.g. `todo_RVCE25MIT015`), preventing data overlap during multi-student lab demos.
* **Premium User Experience:** Designed with glassmorphism, dark-mode toggle, responsive sidebar layout, and animated progress tracking inspired by tools like Notion and Linear.
* **DevOps Lab Integration:** The repository includes pre-configured deployment artifacts (`Dockerfile`, `docker-compose.yml`, `Jenkinsfile`) that students can use immediately to run version control, containerization, automation pipeline, and cloud deployment labs.

---

## 📂 2. Folder Structure

Below is the complete project hierarchy:

```text
todo-app/
├── client/                     # React Frontend (Vite Setup)
│   ├── public/                 # Static Assets
│   ├── src/
│   │   ├── components/         # Reusable UI Components
│   │   │   ├── LoadingScreen.jsx
│   │   │   ├── Sidebar.jsx
│   │   │   ├── TaskCard.jsx
│   │   │   └── TaskModal.jsx
│   │   ├── context/            # React Global State Providers
│   │   │   ├── AuthContext.jsx
│   │   │   └── ThemeContext.jsx
│   │   ├── pages/              # Routed Views
│   │   │   ├── Dashboard.jsx
│   │   │   └── Login.jsx
│   │   ├── utils/              # API Clients & Storage Helpers
│   │   │   ├── api.js
│   │   │   └── todoStorage.js
│   │   ├── App.css
│   │   ├── App.jsx             # React Routing Configuration
│   │   ├── index.css           # Global Tailwind-free CSS Design System
│   │   └── main.jsx            # React Bootstrap Entrypoint
│   ├── index.html              # Frontend Document Template
│   ├── vite.config.js          # Vite Server & Proxy Config
│   └── package.json            # Frontend Package Manifest
├── server/                     # Node.js + Express Backend
│   ├── server.js               # Application Entry & Router
│   ├── users.js                # Hardcoded Lab Student Accounts
│   └── package.json            # Backend Package Manifest
├── Dockerfile                  # Multi-Stage Production Container Build Config
├── docker-compose.yml          # Container Orchestration Spec
├── Jenkinsfile                 # Declarative Pipeline Script
├── .env.example                # Sample Config Variables
├── .gitignore                  # Git Ignore Rules
├── LICENSE                     # Project License
└── package.json                # Root Concurrently Orchestrator Config
```

---

## 💻 3. Software Requirements

Ensure the following environments are installed on the workstation before starting the experiments:

| Software | Purpose | Recommended Version | Download / Install Command |
|---|---|---|---|
| **Node.js** | JavaScript Runtime | `v20.x` or `v22.x` (LTS) | `sudo apt install nodejs` or via NVM |
| **npm** | Package Manager | `v10.x` or higher | Comes packaged with Node.js |
| **Git** | Distributed Version Control | `v2.40.x` or higher | `sudo apt install git` |
| **Docker Engine** | Application Containerization | `v25.x` or higher | [Docker Engine Install Guide](https://docs.docker.com/engine/install/) |
| **Docker Compose** | Multi-container Orchestration | `v2.20.x` or higher | Included in Docker Desktop / apt plugin |
| **Jenkins** | CI/CD Automation Server | `v2.400+` (LTS) | `docker run -p 8080:8080 jenkins/jenkins:lts` |
| **Azure CLI** | cloud Administration | `v2.50.x` or higher | `curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash` |

---

## 🛠️ 4. Installation & Setup

### Step-by-Step Local Deployment
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/Dheeraj-02NK/CNA-Lab-Application.git
   cd CNA-Lab-Application/todo-app
   ```
2. **Setup Configurations:**
   Copy the sample environment variables:
   ```bash
   cp .env.example server/.env
   cp .env.example client/.env
   ```
3. **Install Dependencies:**
   Run the package installer from the root directory. This triggers a post-install hook to configure both client and server directories:
   ```bash
   npm install
   ```
4. **Run the Development Server:**
   Launch the backend server (port 3000) and the Vite frontend (port 5173) simultaneously:
   ```bash
   npm run dev
   ```
5. **Open Browser:**
   Navigate to `http://localhost:5173`. Select any RVCE Student ID (e.g., `RVCE25MIT015`) and login with the password `1234`.

---

# 🧪 DevOps Experiment Guide

---

## Experiment 1: Version Control with Git

### 1.1 Aim
To initialize a local Git repository, track changes, stage modification files, commit snapshots, and review revision histories.

### 1.2 Objective
* Install and configure Git locally.
* Understand the working directory, staging area (index), and local commit repository.
* Stage files and create annotated commits.

### 1.3 Theory
Git is a distributed version control system. Every developer has a complete copy of the project history locally.
* **Working Directory:** Files currently being edited.
* **Staging Area (Index):** A snapshot buffer of changes targeted for the next commit.
* **Repository (.git directory):** Where Git stores commits and configuration metadata.

```
 [Working Directory] ───git add───> [Staging Area] ───git commit───> [Local Repository]
```

### 1.4 Step-by-Step Procedure
1. Open the project root directory in your terminal:
   ```bash
   cd /media/dheeraj/F1/CNA-Lab-Application
   ```
2. Initialize a new Git repository:
   ```bash
   git init
   ```
3. Configure your local developer identity:
   ```bash
   git config --local user.name "Dheeraj N Kashyap"
   git config --local user.email "dheeraj.mit@rvce.edu.in"
   ```
4. Verify the state of files in the directory:
   ```bash
   git status
   ```
5. Add all project files to the staging area:
   ```bash
   git add .
   ```
6. Commit the staged changes to the local repository database:
   ```bash
   git commit -m "feat: initial commit of RVCE Todo App and DevOps configuration files"
   ```
7. Review the commit log:
   ```bash
   git log --oneline
   ```

### 1.5 Expected Output
Running `git log` should output a single commit entry showing your commit hash, author details, date, and commit message:
```text
6f2415e (HEAD -> main) feat: RVCE Todo App - React + Node.js + DevOps ready
```

### 1.6 Troubleshooting Common Errors
* **Error:** `Fatal: not a git repository (or any of the parent directories)`
  * **Cause:** Running Git commands outside the initialized project folder.
  * **Fix:** Ensure you run `cd /path/to/project` first, followed by `git init`.
* **Error:** `Author identity unknown`
  * **Cause:** Git user configurations have not been set.
  * **Fix:** Execute the `git config` command lines shown in step 3 above.

### 1.7 Viva-Voce Questions
1. **What is the difference between `git reset` and `git checkout`?**
   * *Answer:* `git reset` shifts the current branch reference head backward in history or unstages changes. `git checkout` switches between branches or restores working tree files.
2. **What does the command `git add .` do?**
   * *Answer:* Stages all modified, new, and deleted files within the current directory path.
3. **What is the purpose of the staging area in Git?**
   * *Answer:* It acts as a commit preparation buffer where you can review, add, or remove changes before saving them.
4. **How do you discard changes in a local file before staging it?**
   * *Answer:* Run `git checkout -- <filename>` or `git restore <filename>`.
5. **How does Git differ from centralized version control systems like SVN?**
   * *Answer:* Git stores the entire project history on every client machine, allowing offline operations and fast branching/merging, unlike centralized systems.

---

## Experiment 2: Collaborative Development with GitHub

### 2.1 Aim
To configure a remote repository on GitHub, map the local repository to the remote origin, push branches, and clone repositories.

### 2.2 Objective
* Share code across machines using GitHub.
* Setup remote tracking branches.
* Clone remote codebases to distinct workspace folders.

### 2.3 Theory
GitHub is a cloud platform for hosting Git repositories. Working with remote repositories requires registering remote URLs under aliases (conventionally `origin`), linking local branch tracking configurations, and pushing/pulling branches to synchronize revisions.

```
 [Local Machine] ───git push───> [GitHub Remote Origin] ───git clone───> [Colleague Machine]
```

### 2.4 Step-by-Step Procedure
1. Create a public repository named `CNA-Lab-Application` on GitHub.
2. Set the default local branch to `main`:
   ```bash
   git branch -M main
   ```
3. Map the local repository to the remote GitHub target:
   ```bash
   git remote add origin https://github.com/Dheeraj-02NK/CNA-Lab-Application.git
   ```
4. Push your local main branch commit up to GitHub:
   ```bash
   git push -u origin main
   ```
5. Clone the repository in a different folder to verify:
   ```bash
   git clone https://github.com/Dheeraj-02NK/CNA-Lab-Application.git /tmp/test-clone
   ```

### 2.5 Expected Output
Push logs showing successful transfer of objects and reference creations:
```text
To https://github.com/Dheeraj-02NK/CNA-Lab-Application.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

### 2.6 Troubleshooting Common Errors
* **Error:** `Remote origin already exists`
  * **Cause:** The repository already has a remote origin configured.
  * **Fix:** Run `git remote remove origin` first, then run the add command.
* **Error:** `Support for password authentication was removed`
  * **Cause:** GitHub requires SSH keys or Personal Access Tokens (PATs) instead of raw passwords.
  * **Fix:** Generate a Personal Access Token in GitHub Settings -> Developer Settings -> Personal Access Tokens and use it as your password.

### 2.7 Viva-Voce Questions
1. **What does the `-u` flag in `git push -u origin main` do?**
   * *Answer:* It configures upstream tracking for the local branch, allowing future pushes/pulls to run with just `git push` or `git pull`.
2. **What is the difference between `git fetch` and `git pull`?**
   * *Answer:* `git fetch` downloads remote updates without merging them. `git pull` fetches remote updates and automatically merges them into the current branch.
3. **What is a "Fork" in GitHub?**
   * *Answer:* A complete copy of another user's repository saved under your own GitHub account.
4. **How do you resolve a merge conflict?**
   * *Answer:* Open the conflicting files, locate the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`), choose the correct lines, save, stage the files with `git add`, and run `git commit`.
5. **What is a Pull Request (PR)?**
   * *Answer:* A GitHub feature that lets you notify team members about changes you pushed to a branch, allowing them to review and approve the code before it is merged.

---

## Experiment 3: Containerization with Docker & Docker Compose

### 3.1 Aim
To package the React + Node.js application into a production-ready container using a multi-stage `Dockerfile`, and orchestrate it with `docker-compose.yml`.

### 3.2 Objective
* Understand multi-stage container builds.
* Build lightweight Docker images.
* Expose and map container ports.
* Execute multi-container environments using Docker Compose.

### 3.3 Theory
A Docker image is a read-only template with instructions for creating a Docker container.
* **Multi-Stage Build:** Uses multiple `FROM` instructions in a single Dockerfile. Early stages compile assets (like building the React project), and later stages copy only the compiled assets. This keeps compile-time tools out of the final image, reducing its size.
* **Docker Compose:** A tool for defining and running multi-container applications. It uses a YAML file to configure services, networks, and ports.

```
 [Stage 1: React Builder] ──(Compiles /app/client/dist)──> [Stage 2: Production Server]
                                                            └─ Copies build assets
                                                            └─ Runs lightweight Express server
```

### 3.4 Dockerfile Explanation
Our project's `Dockerfile` is structured as follows:
* **Stage 1 (Builder):** Uses `node:20-alpine`, installs frontend dependencies, and runs `npm run build` to generate static files in `client/dist`.
* **Stage 2 (Runtime):** Uses a clean `node:20-alpine` base image, installs only production dependencies for the Express backend, copies compiled static assets from Stage 1, sets env vars, and starts the server.

### 3.5 Step-by-Step Procedure
1. Navigate to the folder containing the `Dockerfile`:
   ```bash
   cd /media/dheeraj/F1/CNA-Lab-Application/todo-app
   ```
2. Build the Docker image:
   ```bash
   docker build -t rvce-todo-app:1.0.0 .
   ```
3. Verify the image was created:
   ```bash
   docker images | grep rvce-todo-app
   ```
4. Run the container:
   ```bash
   docker run -d -p 3000:3000 --name todo-container rvce-todo-app:1.0.0
   ```
5. Check the status of the container:
   ```bash
   docker ps
   ```
6. Verify the app works by calling the health endpoint:
   ```bash
   curl http://localhost:3000/api/health
   ```
7. Stop the running container:
   ```bash
   docker stop todo-container
   docker rm todo-container
   ```
8. Start the application using Docker Compose:
   ```bash
   docker compose up -d
   ```
9. Stop the environment using Docker Compose:
   ```bash
   docker compose down
   ```

### 3.6 Expected Output
Running `docker ps` should show the active container mapping host port 3000 to container port 3000:
```text
CONTAINER ID   IMAGE                 COMMAND                  STATUS                   PORTS
a1b2c3d4e5f6   rvce-todo-app:1.0.0   "docker-entrypoint.s…"   Up 12 seconds (healthy)  0.0.0.0:3000->3000/tcp
```

### 3.7 Troubleshooting Common Errors
* **Error:** `Port 3000 is already in use`
  * **Cause:** A local process (like `npm run dev`) or another container is already using port 3000.
  * **Fix:** Find and stop the process, or run the container on a different port:
    ```bash
    docker run -d -p 8080:3000 --name todo-container rvce-todo-app:1.0.0
    ```

### 3.8 Viva-Voce Questions
1. **Why do we use multi-stage Docker builds?**
   * *Answer:* To reduce image sizes by keeping compilation tools (like compilers and dev dependencies) out of the final runtime image.
2. **What is the difference between an Image and a Container?**
   * *Answer:* An image is a read-only blueprint containing the application and its dependencies. A container is a running instance of an image.
3. **What is the purpose of the `EXPOSE` command in a Dockerfile?**
   * *Answer:* It acts as documentation, letting users know which ports the containerized application listens on. It does not map ports to the host machine.
4. **What is the difference between `CMD` and `RUN` instructions in a Dockerfile?**
   * *Answer:* `RUN` executes commands during the image build stage and saves the resulting layers. `CMD` defines the command that runs when the container starts.
5. **How does the `restart: unless-stopped` directive work in Docker Compose?**
   * *Answer:* It automatically restarts a container if it crashes or the daemon restarts, unless the container was manually stopped.

---

## Experiment 4: CI/CD Pipeline Automation with Jenkins

### 4.1 Aim
To configure a Declarative Jenkins CI/CD pipeline using a `Jenkinsfile` to pull, build, and verify the application.

### 4.2 Objective
* Understand Continuous Integration and Continuous Delivery (CI/CD) pipelines.
* Configure a pipeline in Jenkins.
* Execute a Declarative pipeline defined in code (`Jenkinsfile`).

### 4.3 Theory
Jenkins is an automation server. A pipeline is a group of stages that build, test, and deliver applications.
* **Declarative Pipeline:** A clean way to define pipelines using code (`Jenkinsfile`) with structured blocks (`pipeline`, `agent`, `stages`, `steps`).
* **SCM (Source Control Management):** Tells Jenkins to pull the pipeline definition directly from Git.

```
 [Git Push] ──> [Jenkins Trigger] ──> [Stage: Build] ──> [Stage: Test] ──> [Stage: Verify]
```

### 4.4 Step-by-Step Procedure
1. Start Jenkins locally using Docker:
   ```bash
   docker run -d -p 8080:8080 -p 50000:50000 --name jenkins -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
   ```
2. Open Jenkins in your browser at `http://localhost:8080`. Retrieve the administrator key:
   ```bash
   docker logs jenkins
   ```
3. Complete the setup wizard and install the default plugins.
4. Click **New Item**, enter `rvce-todo-app`, select **Pipeline**, and click **OK**.
5. Scroll down to the **Pipeline** section:
   * **Definition:** Select *Pipeline script from SCM*.
   * **SCM:** Select *Git*.
   * **Repository URL:** Enter `https://github.com/Dheeraj-02NK/CNA-Lab-Application.git`.
   * **Branch:** Change from `*/master` to `*/main`.
   * **Script Path:** Enter `todo-app/Jenkinsfile` (pointing to the pipeline configuration in the subfolder).
6. Click **Save**.
7. Click **Build Now** to trigger the build.
8. Click the active build number and open the **Console Output** to monitor progress.

### 4.5 Expected Output
A successful build pipeline showing all completed stages:
```text
[Pipeline] { (Checkout)
[Pipeline] sh (📥 Checking out source code...)
...
[Pipeline] { (Install Dependencies)
...
[Pipeline] { (Build Application)
...
[Pipeline] { (Verify Build)
...
[Pipeline] Stage Complete: Pipeline Complete
[Pipeline] Finished: SUCCESS
```

### 4.6 Troubleshooting Common Errors
* **Error:** `npm: command not found`
  * **Cause:** Node.js is not installed on the agent machine running Jenkins.
  * **Fix:** Install Node.js on the agent, or configure the Node.js plugin in Jenkins Global Tool Configuration.

### 4.7 Viva-Voce Questions
1. **What is a declarative pipeline in Jenkins?**
   * *Answer:* A structured way to define a pipeline as code using a specific schema, making it easier to read and maintain.
2. **What does the `agent any` directive mean?**
   * *Answer:* Tells Jenkins to run the pipeline on any available executor agent.
3. **What is the difference between CI and CD?**
   * *Answer:* CI (Continuous Integration) is the practice of automatically building and testing changes when developers push code. CD (Continuous Delivery/Deployment) automatically prepares the built application for release or deploys it to production.
4. **How does Jenkins locate the pipeline definition when using SCM?**
   * *Answer:* It pulls the Git repository and reads the `Jenkinsfile` at the path configured in the job settings.
5. **What are post-build actions in a pipeline?**
   * *Answer:* Steps that run after the pipeline completes, depending on whether it succeeded, failed, or was aborted (configured in the `post` block).

---

## Experiment 5: Cloud Deployment on Azure App Service

### 5.1 Aim
To deploy the React + Node.js application to Microsoft Azure App Service and configure automated deployments from GitHub.

### 5.2 Objective
* Configure Web Apps in the Azure Cloud Portal.
* Link GitHub repositories to Azure Deployment Center.
* Verify deployment using the health check endpoint.

### 5.3 Theory
Azure App Service is a PaaS (Platform as a Service) offering for hosting web applications. By linking a GitHub repository, Azure configures a deployment pipeline that triggers a build and deploy flow whenever code is pushed to the main branch.

```
 [Developer Push] ──> [GitHub Actions Build] ──> [Azure App Service Deployment Engine]
```

### 5.4 Step-by-Step Procedure
1. Log in to the [Azure Portal](https://portal.azure.com).
2. Click **Create a resource**, search for **Web App**, and click **Create**:
   * **Resource Group:** Create new (e.g. `rg-rvce-devops`).
   * **Name:** Choose a unique domain name (e.g. `rvce-todo-app-dheeraj`).
   * **Publish:** Select *Code*.
   * **Runtime stack:** Select *Node 20 LTS*.
   * **Operating System:** Select *Linux*.
   * **Region:** Choose a close region (e.g. *Central India* or *East US*).
3. Click **Review + Create**, then click **Create**.
4. Once deployment completes, open the resource and navigate to the **Deployment Center** in the left menu.
5. Under settings, select **GitHub** as the source and authorize Azure to access your account.
6. Select your organization, repository (`CNA-Lab-Application`), and branch (`main`).
7. Click **Save**. This generates a GitHub Actions workflow file in your repository.
8. Go to **Configuration** (under Settings) and add a new application setting:
   * **Name:** `PORT`
   * **Value:** `3000`
9. Under General Settings, set the startup command:
   ```bash
   npm run build && npm start
   ```
10. Monitor the build in your GitHub repository's **Actions** tab. Once completed, browse to your Azure site URL.

### 5.5 Expected Output
Accessing `https://<your-web-app-name>.azurewebsites.net/api/health` should return:
```json
{
  "status": "Running",
  "application": "RVCE Todo App",
  "version": "1.0.0"
}
```

### 5.6 Troubleshooting Common Errors
* **Error:** `Application Error: (Ref: 502 Bad Gateway / Timeout)`
  * **Cause:** The App Service did not start within the timeout limit because it couldn't locate the startup script or build assets.
  * **Fix:** Verify your startup command is set to `npm run build && npm start` and the port configuration matches.

### 5.7 Viva-Voce Questions
1. **What is PaaS in cloud computing?**
   * *Answer:* Platform as a Service (PaaS) provides a managed environment for developing, testing, and deploying applications without having to manage the underlying server infrastructure.
2. **What does the Azure Deployment Center do?**
   * *Answer:* It automates the CI/CD pipeline, linking source control (like GitHub or Bitbucket) directly to the Web App.
3. **How does Azure App Service route traffic to your Node.js application?**
   * *Answer:* It uses a reverse proxy to route incoming HTTP traffic on port 80/443 to the port your application is listening on.
4. **Why is it important to set environment variables in the Azure Portal Configuration tab?**
   * *Answer:* Setting variables in the portal separates configuration from code, keeping secrets out of public source control repositories.
5. **How can you view live console logs from an Azure App Service?**
   * *Answer:* Go to the Web App's left menu, select **Log Stream**, and turn on Application Logging.

---

## Experiment 6: Intentionally Omitted
> **Note:** Experiment 6 is intentionally omitted from this guide because it is designed as an internal laboratory test and assessment.

---

## Experiment 7: DevOps Foundational Lifecycle & Workflow

### 7.1 Aim
To analyze the DevOps lifecycle, understand Continuous Integration/Continuous Deployment (CI/CD) pipelines, and examine how code moves from local development to production.

### 7.2 Theory
DevOps is a set of practices that combines software development (Dev) and IT operations (Ops) to shorten the development lifecycle and deliver high-quality software continuously.

```
                   [PLAN] ──> [CODE] ──> [BUILD] ──> [TEST]
                     ▲                                 │
                     │                                 ▼
                  [MONITOR] <── [OPERATE] <── [DEPLOY] <── [RELEASE]
```

### 7.3 The DevOps Lifecycle
* **Plan:** Plan tasks and track issues (using tools like Jira, GitHub Projects, or Trello).
* **Code:** Developers write code and use version control (Git) to merge changes.
* **Build:** Automated build tools package the application (Docker images, npm builds).
* **Test:** Run automated suites to verify code quality.
* **Release:** Prepare the application for deployment (artifacts, package versioning).
* **Deploy:** Deploy built assets to cloud environments (Azure App Service, Kubernetes).
* **Operate:** Maintain running infrastructure and scale applications.
* **Monitor:** Track application health, performance metrics, and logs (using Prometheus, Grafana, or Azure Monitor).

### 7.4 Viva-Voce Questions
1. **What is the main goal of DevOps?**
   * *Answer:* To improve collaboration between development and operations teams, automate release pipelines, and speed up software delivery while maintaining quality.
2. **What is the difference between Continuous Delivery and Continuous Deployment?**
   * *Answer:* Continuous Delivery automates building, testing, and staging, but requires manual approval to deploy to production. Continuous Deployment automatically deploys every successful build to production without manual intervention.
3. **What is Infrastructure as Code (IaC)?**
   * *Answer:* The practice of managing and provisioning IT infrastructure using configuration files (like Terraform or CloudFormation) rather than manual processes.
4. **Why is feedback important in the DevOps cycle?**
   * *Answer:* Continuous feedback from monitoring and logs helps developers quickly identify bugs, improve performance, and align features with user needs.
5. **What is the role of a container orchestrator like Kubernetes?**
   * *Answer:* It automates the deployment, scaling, management, and networking of containerized applications.

---

## Experiment 8: DevSecOps

### 8.1 Aim
To integrate security practices into the DevOps pipeline (DevSecOps) by implementing early vulnerability checks, scanning dependencies, and protecting secrets.

### 8.2 Theory
DevSecOps is the practice of integrating security early in the software development lifecycle, rather than checking it only at the end. This is known as **Shift-Left Security**.

```
 Traditional:  [Design] ──> [Code] ──> [Build] ──> [Deploy] ──> [Security Audit] ❌ (Late)
 DevSecOps:    [Design] ──> [Security] ──> [Code + Scan] ──> [Build + Verify] ──> [Deploy]  (Shift-Left)
```

### 8.3 DevSecOps Practices
* **Static Application Security Testing (SAST):** Scans source code for security patterns and vulnerabilities before compiling it.
* **Dynamic Application Security Testing (DAST):** Analyzes running applications to find vulnerabilities (like SQL injection or cross-site scripting) at runtime.
* **Software Composition Analysis (SCA):** Scans third-party libraries and dependencies for known vulnerabilities (e.g., using `npm audit` or Snyk).
* **Secrets Scanning:** Checks commits for hardcoded passwords, tokens, or private keys to prevent them from being pushed to public repositories.

### 8.4 Implementing DevSecOps in this Project
1. **Run Dependency Vulnerability Scans:**
   Detect vulnerable packages in the node dependencies:
   ```bash
   cd todo-app/server && npm audit
   cd ../client && npm audit
   ```
2. **Verify Secrets in Git History:**
   Ensure no active environment configuration secrets are tracked in Git. Check tracked files against the `.gitignore` rules.

### 8.5 Viva-Voce Questions
1. **What does "Shift-Left" mean in DevSecOps?**
   * *Answer:* Moving security practices and testing earlier in the software development process, rather than checking for security issues right before release.
2. **What is the difference between SAST and DAST?**
   * *Answer:* SAST analyzes raw source code offline. DAST tests running applications from the outside to find vulnerabilities at runtime.
3. **Why should you avoid hardcoding credentials in code?**
   * *Answer:* Hardcoded credentials can easily be leaked in public repositories, giving attackers access to databases and services.
4. **What is the purpose of `npm audit`?**
   * *Answer:* It scans your project's dependency tree for packages with known security vulnerabilities and recommends fixes.
5. **What is a false positive in security scans?**
   * *Answer:* An issue flagged by a scanning tool that is actually safe and does not pose a security risk in your environment.

---

## Experiment 9: GitHub Webhooks for Automated Jenkins Triggering

### 9.1 Aim
To configure a GitHub Webhook to notify a local Jenkins instance of push events, triggering automated builds.

### 9.2 Objective
* Understand Webhook mechanisms.
* Expose local Jenkins ports using Ngrok (or local setup equivalent).
* Configure GitHub triggers for CI/CD pipelines.

### 9.3 Theory
A Webhook is an HTTP POST request triggered by an event on a source system (like pushing code to GitHub) that sends data to a destination system (like Jenkins) in real-time.

```
 [git push] ──> [GitHub Event] ──(HTTP POST Webhook)──> [ngrok Tunnel] ──> [Jenkins Server] ──> [Auto Build]
```

### 9.4 Step-by-Step Procedure
1. If your Jenkins instance is running locally (`http://localhost:8080`), make it accessible from the internet. Run an ngrok tunnel on port 8080:
   ```bash
   ngrok http 8080
   ```
   Copy the secure forwarding URL (e.g. `https://a1b2-34-56-78.ngrok-free.app`).
2. Go to your GitHub repository, click **Settings**, and select **Webhooks** from the left menu.
3. Click **Add Webhook**:
   * **Payload URL:** Paste your ngrok URL and append the Jenkins GitHub hook path:
     `https://<your-ngrok-subdomain>.ngrok-free.app/github-webhook/`
   * **Content Type:** Select `application/json`.
   * **Trigger events:** Select *Just the push event*.
4. Click **Add Webhook**. Verify you get a green checkmark next to the webhook in GitHub, indicating a successful ping connection.
5. Go to your Jenkins Dashboard -> select the `rvce-todo-app` pipeline -> click **Configure**.
6. Under **Build Triggers**, check the box for **GitHub hook trigger for GITSCM polling**.
7. Click **Save**.
8. Make a small text change in your local project code (e.g. in the `README.md`), stage it, commit, and push it to GitHub:
   ```bash
   git add README.md
   git commit -m "docs: test automated trigger"
   git push origin main
   ```
9. Verify that a new build starts automatically in Jenkins without manual intervention.

### 9.5 Expected Output
Checking the Jenkins build list should show a new build triggered by a GitHub push event:
```text
Build #3 (Jun 26, 2026 8:50 PM)
Started by GitHub push by Dheeraj-02NK
```

### 9.6 Troubleshooting Common Errors
* **Error:** Webhook returns a `403 Forbidden` status.
  * **Cause:** Jenkins security options prevent anonymous webhook requests.
  * **Fix:** Go to Jenkins -> Manage Jenkins -> Security -> verify authorization settings permit webhook requests, or configure GitHub integration tokens.

### 9.7 Viva-Voce Questions
1. **What is a webhook?**
   * *Answer:* An automated HTTP callback triggered by a specific event (like a push or commit) that sends real-time data to another system.
2. **What is the difference between Webhooks and Polling?**
   * *Answer:* Polling requires Jenkins to check the Git repository at scheduled intervals. Webhooks notify Jenkins immediately when an event occurs, saving resources.
3. **Why do we need tools like ngrok when testing webhooks locally?**
   * *Answer:* GitHub cannot reach local addresses (like `localhost` or `127.0.0.1`) directly. Ngrok creates a public URL that tunnels traffic to your local port.
4. **What is the purpose of appending `/github-webhook/` to the Jenkins payload URL?**
   * *Answer:* It points to the endpoint exposed by the Jenkins GitHub integration plugin that handles incoming push notifications.
5. **How can you verify if a webhook request was sent by GitHub?**
   * *Answer:* GitHub signs webhook payloads using a secret key, sending the signature in the `X-Hub-Signature-256` header for validation.

---

## 🔌 6. API Documentation

### 1. Health Status API
* **Endpoint:** `GET /api/health`
* **Purpose:** Verification endpoint for Docker health checks, Jenkins validation steps, and cloud probes.
* **Sample Request:**
  ```bash
  curl http://localhost:3000/api/health
  ```
* **Sample Response:**
  ```json
  {
    "status": "Running",
    "application": "RVCE Todo App",
    "version": "1.0.0",
    "timestamp": "2026-06-26T15:10:00.000Z",
    "uptime": 12.34,
    "environment": "production"
  }
  ```

### 2. Login API
* **Endpoint:** `POST /api/login`
* **Purpose:** Authenticates a student using their RVCE ID.
* **Sample Request:**
  ```bash
  curl -X POST http://localhost:3000/api/login \
       -H "Content-Type: application/json" \
       -d '{"rvceId": "RVCE25MIT015", "password": "1234"}'
  ```
* **Sample Response (Success):**
  ```json
  {
    "success": true,
    "name": "DHEERAJ N KASHYAP",
    "rvceId": "RVCE25MIT015"
  }
  ```

---

## 🚨 7. Comprehensive Troubleshooting Manual

Below is a troubleshooting guide for common issues you might encounter in the lab:

| # | Problem | Possible Cause | Solution |
|---|---|---|---|
| 1 | `npm install` fails | Node.js version mismatch or outdated npm cache. | Run `npm cache clean --force` and ensure you are using Node.js v20+. |
| 2 | `Port 3000 already in use` | Another process is listening on the Express server port. | Kill the process using `sudo kill -9 $(lsof -t -i:3000)` or change the port in `.env`. |
| 3 | React page is blank | Frontend failed to compile or the Vite proxy configuration is broken. | Check the browser console logs and verify the `vite.config.js` settings. |
| 4 | `git push` rejected | Remote repository has changes not present in the local clone. | Run `git pull origin main` to fetch and merge changes before pushing. |
| 5 | Docker build fails | Missing files or incorrect paths in the Dockerfile. | Verify directory context settings: `docker build -t todo-app .` must be run from the root. |
| 6 | Container exits immediately | Port mapping errors or configuration script failures. | Run `docker logs <container-id>` to check the application crash logs. |
| 7 | Jenkins build hangs | Node/npm path configurations are missing or incorrect on the agent. | Ensure Node.js paths are correctly set in the Jenkins Global Tool Configuration. |
| 8 | Webhook returns `404` | Incorrect payload URL path in the GitHub repository settings. | Ensure the URL ends with a trailing slash: `.../github-webhook/`. |
| 9 | Azure site returns `502` | App Service failed to start within the timeout limit. | Add the startup command: `npm run build && npm start` in Configuration settings. |
| 10 | Docker Compose build fails | Docker daemon is not running. | Start the service using `sudo systemctl start docker`. |
| 11 | LocalStorage is empty | Browser private browsing mode is blocking local storage access. | Use a regular browser window and ensure cookies and site storage permissions are enabled. |
| 12 | API requests fail with `ERR_CONNECTION_REFUSED` | Express server is stopped or crashing. | Run `npm run server` to check the backend status. |
| 13 | CSS styles are missing | CSS file import paths are incorrect. | Verify `index.css` is imported in `main.jsx` and imports are resolved. |
| 14 | `Permission denied` on Docker commands | User is not in the system's docker group. | Run commands with `sudo` prefix or add your user to the group: `sudo usermod -aG docker $USER`. |
| 15 | Jenkins pipeline fails at checkout | Invalid GitHub credentials or incorrect branch name. | Verify the branch name matches the remote: `main`. |
| 16 | Vite proxy returns `504 Gateway Timeout` | Express server is stopped or unresponsive. | Ensure the backend is running on port 3000. |
| 17 | `Cannot find module` error | Dependencies were not fully installed. | Run `npm run install:all` to reinstall node modules. |
| 18 | `docker-compose` command not found | Missing Docker Compose installation. | Install the docker-compose-plugin: `sudo apt install docker-compose-plugin`. |
| 19 | Git log shows incorrect author | Git user configurations are unset or configured globally for a different account. | Run `git config --local user.name "Your Name"` to override settings locally. |
| 20 | Changes don't show up in Docker | Running a container from an old cached image layer. | Rebuild the image without cache: `docker build --no-cache -t todo-app .`. |

---

## ❓ 8. Frequently Asked Questions

### Git & GitHub
1. **Can I use git on directories without running `git init`?**
   * No, a folder must contain a `.git` control subdirectory to run Git commands.
2. **What does `.gitignore` do?**
   * It tells Git to ignore matching files (like `node_modules` or `.env` files) so they aren't tracked or committed.
3. **How do I delete a Git branch locally and remotely?**
   * Delete locally: `git branch -d <branch_name>`. Delete remotely: `git push origin --delete <branch_name>`.
4. **What is a commit hash?**
   * A unique SHA-1 identifier for a commit, calculated from the changes, author, and timestamp.
5. **How do I undo the most recent commit?**
   * Run `git reset --soft HEAD~1` to undo the commit while keeping your changes staged.

### Docker & Containerization
6. **What makes Docker different from virtual machines?**
   * Virtual machines bundle a complete guest OS. Docker containers share the host OS kernel, making them much faster and lighter.
7. **What is a Docker base image?**
   * A pre-built image (like `node:20-alpine`) used as the starting layer in a `Dockerfile`.
8. **Why are Alpine Linux images popular in Dockerfiles?**
   * Alpine images are minimal (around 5MB), which helps keep the final container size small.
9. **How do I list all running and stopped containers?**
   * Run `docker ps -a`.
10. **What is the purpose of volume mapping (`-v`)?**
    * It mounts a host directory inside a container, letting you persist data even if the container is deleted.

### Jenkins & CI/CD
11. **What is the difference between a Jenkins pipeline and a freestyle project?**
    * Freestyle projects use a GUI to configure builds. Pipelines define steps in code (a `Jenkinsfile`), which can be tracked in version control.
12. **Can a pipeline run stages in parallel?**
    * Yes, you can use the `parallel` block to run tasks concurrently on multiple executors.
13. **How do you configure Jenkins to poll Git repositories periodically?**
    * Go to Pipeline settings, enable **Poll SCM**, and configure a cron expression (e.g. `H/5 * * * *` to poll every 5 minutes).
14. **What does the `sh` step do in a Jenkinsfile?**
    * It executes a shell command on the agent running the pipeline.
15. **How can you store secure credentials in Jenkins?**
    * Go to Manage Jenkins -> Credentials to store keys, passwords, and certificates securely.

### Azure Deployment
16. **Why does Azure App Service require a startup command?**
    * It needs to know how to start your Node.js application after deploying the code.
17. **What is Kudu in Azure App Service?**
    * Kudu is the engine behind Git deployments in Azure, providing tools like a web SSH terminal and file explorer.
18. **Does Azure App Service scale automatically?**
    * Yes, you can configure scaling rules based on CPU usage or traffic load.
19. **What is the difference between deployment slots?**
    * Slots are separate instances of your app with their own hostnames, letting you test changes before swapping them into production.
20. **Can I deploy Docker containers to Azure Web Apps?**
    * Yes, select the Docker Container option instead of Code when creating the Web App.

---

## 🎓 9. Top 50 Viva-Voce Questions & Answers

### Git & Version Control
1. **What is Git?**
   * A distributed version control system for tracking changes in source code during software development.
2. **What does `git clone` do?**
   * Downloads an existing repository and its entire history from a remote server to a local folder.
3. **What is the purpose of `git status`?**
   * Shows the state of the working directory and staging area, listing modified, deleted, or untracked files.
4. **How does `git commit` work?**
   * Saves a snapshot of staged changes to the local repository history.
5. **What is the difference between `git reset --soft` and `git reset --hard`?**
   * `--soft` undoes the commit but leaves your changes staged. `--hard` discards the commit and all changes in the working directory.
6. **What is the Head in Git?**
   * A reference pointer to the current branch head or commit in your workspace.
7. **What is a merge conflict?**
   * Occurs when changes on different branches modify the same line of a file, requiring manual review to resolve.
8. **What does `git rebase` do?**
   * Applies commits from one branch on top of another, keeping the commit history clean.
9. **Explain the staging area.**
   * A file index that holds changes scheduled for the next commit.
10. **How do you configure a global Git username?**
    * Run `git config --global user.name "Your Name"`.

### Docker
11. **What is Docker?**
    * An open-source platform for building, shipping, and running applications inside containers.
12. **What is containerization?**
    * Packaging an application and all its dependencies together in a single container, ensuring it runs reliably on any environment.
13. **What is a Dockerfile?**
    * A text document containing instructions to assemble a Docker image.
14. **What is the difference between `ADD` and `COPY` in a Dockerfile?**
    * `COPY` duplicates local files. `ADD` can also download files from remote URLs and extract tar archives.
15. **What is Docker Hub?**
    * A public cloud registry for sharing and downloading container images.
16. **How do you stop a running container?**
    * Run `docker stop <container_id>`.
17. **What does the `-p` flag do?**
    * Maps a host port to a container port (e.g. `-p 3000:3000`).
18. **What is the purpose of `.dockerignore`?**
    * Prevents local files (like build artifacts or `node_modules`) from being copied into the Docker build context.
19. **How do you remove unused Docker images?**
    * Run `docker image prune`.
20. **What is Docker Compose?**
    * A tool for defining and running multi-container Docker applications using a YAML configuration file.

### Jenkins
21. **What is Jenkins?**
    * An open-source automation server used to build, test, and deploy software.
22. **What is a CI/CD pipeline?**
    * An automated workflow that takes code changes from commit to production.
23. **What is a Jenkinsfile?**
    * A text file containing the definition of a Jenkins pipeline, checked into version control.
24. **Explain the difference between scripted and declarative pipelines.**
    * Scripted pipelines use Groovy code and offer more flexibility. Declarative pipelines use a structured schema that is easier to read and configure.
25. **What are stages in a pipeline?**
    * Blocks that group related tasks together (like Build, Test, or Deploy).
26. **What is a Jenkins Workspace?**
    * A directory on the agent where Jenkins pulls source code and runs build tasks.
27. **What is a build trigger?**
    * An event (like a webhook, schedule, or manual click) that starts a pipeline build.
28. **How does Jenkins integrate with Git?**
    * Using the Git plugin, which pulls code from remote repositories during the pipeline's checkout stage.
29. **What are executors in Jenkins?**
    * Threads on an agent node that run pipeline steps.
30. **What is the purpose of Jenkins plugins?**
    * Plugins extend Jenkins' core features, adding integrations with third-party tools like Docker, Git, and Slack.

### Cloud & Azure
31. **What is cloud computing?**
    * Delivering computing services (like servers, storage, databases, and networking) over the internet.
32. **What is Azure App Service?**
    * A cloud service for hosting web applications and REST APIs without managing infrastructure.
33. **What is deployment slot swapping in Azure?**
    * Swapping staging and production slots to deploy updates with zero downtime.
34. **What is Azure Resource Group?**
    * A container that holds related resources for an Azure solution.
35. **What is SaaS?**
    * Software as a Service (SaaS) delivers cloud-based applications over the internet (like Office 365 or Gmail).
36. **Explain IaaS.**
    * Infrastructure as a Service (IaaS) provides virtualized computing resources (like VMs and storage) over the internet.
37. **What is Azure Deployment Center?**
    * A tool in the Azure portal for setting up automated deployments from source control platforms like GitHub.
38. **How does Azure secure application settings?**
    * By encrypting App Settings, keeping credentials out of public repositories.
39. **What are Azure web jobs?**
    * Background tasks (like scripts or programs) that run in the same context as your Web App.
40. **What is Azure App Service Plan?**
    * Defines the region, instance size, scale count, and pricing tier for a Web App.

### DevOps
41. **What is DevOps?**
    * A set of practices that combines development and operations to shorten release cycles.
42. **What is DevSecOps?**
    * Integrating security practices early in the DevOps lifecycle.
43. **Explain Continuous Integration.**
    * Automatically building and testing code changes whenever developers merge changes into a shared repository.
44. **What is Continuous Deployment?**
    * Automatically deploying code changes to production after they pass testing.
45. **What is GitOps?**
    * Using Git repositories as the single source of truth for infrastructure configuration and deployment states.
46. **What is a Webhook?**
    * An automated HTTP notification sent from one system to another when an event occurs.
47. **What does shift-left security mean?**
    * Finding and fixing security issues early in the development process, reducing security risks.
48. **What is SAST?**
    * Static Application Security Testing, which scans source code for vulnerabilities before compiling it.
49. **What is Software Composition Analysis (SCA)?**
    * Scanning project dependencies for known security vulnerabilities.
50. **What is container orchestration?**
    * Automating the deployment, scaling, and management of containerized applications.

---

## 🚀 10. Future Enhancements & Project Scope

Future additions for advanced labs could include:
1. **Persistent Databases:** Move from `localStorage` to dedicated SQLite or PostgreSQL container instances.
2. **JWT-Based Authentication:** Implement JSON Web Tokens for secure session management.
3. **Role-Based Access Control (RBAC):** Add roles (student, instructor, administrator) to show different dashboard views.
4. **Kubernetes Integration:** Add manifests to deploy and scale the application on Kubernetes.
5. **ELK Logging Stack:** Set up Elasticsearch, Logstash, and Kibana to collect and analyze container logs.

---

## 🏁 11. Conclusion

This project serves as a complete sandbox for college DevOps labs. By working with this single repository, students get hands-on experience with:
* Tracking changes and collaborating with **Git & GitHub**.
* Containerizing applications with **Docker & Docker Compose**.
* Automating workflows with **Jenkins**.
* Hosting projects in the cloud with **Azure App Service**.
* Triggering automated builds using **GitHub Webhooks**.
