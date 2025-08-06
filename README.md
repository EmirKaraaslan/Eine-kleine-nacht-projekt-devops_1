# 🐳 CI/CD Pipeline for Node.js Microservice on AWS EKS

This project implements a production-grade **CI/CD pipeline** using:
- 🐙 **GitHub Actions** for automation
- 🐳 **Docker** for containerization
- 🏷️ **AWS ECR** as image registry
- ☸️ **Kubernetes (EKS)** for orchestration
- 🎯 **Helm** for deployment

---

## 🚀 Tech Stack

| Tool            | Purpose                                 |
|-----------------|------------------------------------------|
| Node.js         | Sample microservice                     |
| Docker          | Containerization                        |
| AWS ECR         | Docker image registry                   |
| AWS EKS         | Kubernetes cluster                      |
| Helm            | Declarative deployment on K8s           |
| GitHub Actions  | CI/CD pipeline                          |

---

## 📦 Features

- Push to `main` branch triggers:
  - Docker build from `./app`
  - Push image to ECR with unique tag (commit hash)
  - Deploy new image to EKS via Helm
- `imagePullPolicy: Always` ensures latest image is used
- Rollout & rollback compatible via `helm upgrade` & `helm rollback`

---

## 🛠 Folder Structure

.
├── .github/workflows/ # GitHub Actions CI/CD pipeline
├── app/ # Node.js app source code
│ └── index.js
├── helm-chart/ # Helm deployment templates
│ ├── templates/
│ │ ├── deployment.yaml
│ │ └── service.yaml
│ └── values.yaml
└── README.md


## ⚙️ How it works

1. GitHub Action triggers on every `push` to `main`
2. Docker builds the app and tags with commit hash
3. Image is pushed to AWS ECR
4. Helm upgrades the deployment in EKS with new tag
5. Kubernetes performs a **rolling update** to apply the new image

---

## 🧠 Why Kubernetes?

Kubernetes enables:
- 🔄 **Rolling updates**
- ⏪ **Easy rollback**
- 🔒 **Scalability & resilience**
- 🔁 **Zero downtime deployments**
  

## 🔐 Secrets Used

The following secrets must be added to GitHub repo:

| Secret Name              | Description                     |
|--------------------------|----------------------------------|
| `AWS_ACCESS_KEY_ID`      | IAM access key                  |
| `AWS_SECRET_ACCESS_KEY`  | IAM secret                      |
| `AWS_REGION`             | E.g. `eu-central-1`             |
| `AWS_ACCOUNT_ID`         | Your AWS account number         |
| `ECR_REPOSITORY`         | ECR repo name (e.g. `node-service`) |


