# 🔷 GitHub Actions CI/CD – End-to-End Notes (Step by Step)

---

## 1️⃣ What is GitHub Actions?

**GitHub Actions** is a built-in GitHub tool that allows you to automate workflows such as:

- Building applications  
- Running tests  
- Creating Docker images  
- Deploying applications to servers  

It works based on **events** like:

- `push`
- `pull_request`
- `release`

---

## 2️⃣ What is CI/CD?

### 🔹 CI – Continuous Integration

- Automatically builds and tests code  
- Runs whenever code is pushed  
- Ensures code does not break  

### 🔹 CD – Continuous Delivery / Deployment

- Packages the application (Docker image)  
- Makes it deploy-ready  
- Optionally deploys automatically  

---

## 3️⃣ GitHub Actions Workflow Basics

A workflow is defined using a **YAML** file inside:

- .github/workflows/

### Main components

- **Event** – When to run (push, PR)  
- **Job** – What machine to use  
- **Steps** – Commands or actions  

---

## 4️⃣ Project Setup (Context)

The project uses:

- ✅ Java Spring Boot application  
- ✅ Gradle build tool  
- ✅ Docker  
- ✅ Docker Hub  
- ✅ GitHub Actions  

---

## 5️⃣ CI Part – What You Configured

### What happens in CI

1. You push code to GitHub  
2. GitHub Actions starts automatically  
3. Gradle builds the Spring Boot app  
4. `.jar` file is created  

### CI Purpose

- Verify code compiles  
- Catch errors early  
- Ensure stable builds  

✔️ **CI is correctly implemented**

---

## 6️⃣ Docker Integration (CD – Delivery)

### What happens next

1. Dockerfile is used  
2. Docker image is built  
3. Image is tagged as `latest`  
4. Image is pushed to Docker Hub  

### Example

yourname/spring-app:latest

✔️ Docker image is created  
✔️ Docker image is pushed automatically  
✔️ No manual work required  

---

## 7️⃣ Very Important Clarification ❗

### ❓ Is pushing image to Docker Hub = deployed?

❌ **NO**

- Pushing image = application is packaged, not running  
- Deployment happens **only when the container is running on a server**

---

## 8️⃣ Continuous Delivery vs Continuous Deployment

### 🔹 Continuous Delivery (Current Setup)

Code Push
→ Build (CI)
→ Docker Image
→ Push to Docker Hub

✔️ Application is always ready  
❌ Application is not running automatically  

---

### 🔹 Continuous Deployment (Future Enhancement)

Code Push
→ Build
→ Docker Push
→ Pull image on server
→ Stop old container
→ Run new container

✔️ Fully automated  
✔️ Live application updates automatically  

---

## 9️⃣ Meaning of `latest` Tag

- `latest` means **most recent build**  
- Every new push replaces the old image  
- It is **not a version number**

### Better practice (future)

app:v1.0
app:commit-sha
app:latest

---

## 🔟 What Happens in the Future

After everything is configured, you only do:

```bash
git push origin main
```

GitHub Actions automatically:

Builds the Spring Boot app

Rebuilds Docker image

Pushes updated image to Docker Hub

❌ No manual build
❌ No manual Docker push

### 1️⃣1️⃣ One-Time Manual Setup

You must do these only once:

- Create workflow YAML file
- Add Docker Hub credentials as GitHub Secrets
- Write Dockerfile
- After this → Fully automatic

### 1️⃣2️⃣ What Is Missing for FULL Deployment

Docker Hub updated ≠ Application running
To deploy, one of the following is needed:

- SSH into server
- docker pull
- docker run
- Kubernetes or Docker Compose

### 1️⃣3️⃣ Final Pipeline Status

| Stage                  | Status        |
| ---------------------- | ------------  |
| GitHub Actions setup   | ✅            |
| Gradle build           | ✅            |
| Docker image build     | ✅            |
| Docker push            | ✅            |
| Continuous Integration | ✅            |
| Continuous Delivery    | ✅            |
| Continuous Deployment  | ❌ (optional) |

### 1️⃣4️⃣ One-Paragraph Final Explanation

```bash
In a Java Spring Boot application, GitHub Actions can be configured to automatically trigger a CI/CD pipeline whenever code is pushed to the repository. The pipeline builds the application using Gradle, creates a Docker image, and pushes the image to Docker Hub without any manual intervention. This setup represents Continuous Integration and Continuous Delivery. To achieve Continuous Deployment, an additional step is required to automatically pull and run the updated Docker image on a server.
```
