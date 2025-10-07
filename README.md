# WexaAI DevOps Assessment

## **Project Overview**

This repository demonstrates containerizing a Next.js application, automating its build and deployment using **GitHub Actions** and **GitHub Container Registry (GHCR)**, and deploying it to **Kubernetes (Minikube)**.

---

## **Table of Contents**

1. [Next.js Application](#nextjs-application)
2. [Docker](#docker)
3. [CI/CD with GitHub Actions](#cicd-with-github-actions)
4. [Kubernetes Deployment](#kubernetes-deployment)
5. [Accessing the App](#accessing-the-app)
6. [Repository & Image Links](#repository--image-links)

---

## **Next.js Application**

* The application is in the `src/` folder.
* To run locally:

```bash
npm install
npm run dev
```

* The app runs at: [http://localhost:3000](http://localhost:3000)

---

## **Docker**

* Dockerfile is in the root directory.
* Build the Docker image locally:

```bash
docker build -t wexaai-nextjs .
```

* Run the Docker container:

```bash
docker run -p 3000:3000 wexaai-nextjs
```

---

## **CI/CD with GitHub Actions**

* Workflow file: `.github/workflows/ci.yml`
* Triggered automatically on push to `main`.
* Steps:

  1. Checkout repository
  2. Set up Docker Buildx
  3. Login to GitHub Container Registry (GHCR)
  4. Build Docker image
  5. Push image to GHCR

**Docker image URL on GHCR:**

```
ghcr.io/sunloid/wexaai-devops-assessment:latest
```

---

## **Kubernetes Deployment**

* Manifests in `k8s/` folder:

  * `deployment.yaml` – defines pods, replicas, container image, and health checks
  * `service.yaml` – exposes the app using a NodePort

### **Steps to deploy locally (Minikube):**

```bash
minikube start
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
kubectl get pods
kubectl get svc
minikube service nextjs-service
```

* Update deployment when pushing a new image:

```bash
kubectl set image deployment/nextjs-deployment nextjs-app=ghcr.io/sunloid/wexaai-devops-assessment:latest
```

---

## **Accessing the App**

* Locally via browser after `minikube service nextjs-service`.
* Kubernetes exposes it on a NodePort mapped by Minikube.

---

## **Repository & Image Links**

* **GitHub Repository:**

```
https://github.com/sunloid/wexaai-devops-assessment
```

* **GHCR Docker Image:**

```
ghcr.io/sunloid/wexaai-devops-assessment:latest
```

---

This README covers **everything** needed for your assignment — local dev, Docker, CI/CD, and Minikube deployment.

---

If you want, I can also **suggest a clean repo folder structure** so your submission looks professional.

Do you want me to do that?
