# DevOps Starter Kit 🚀

**DevOps starter kit with CI/CD and Kubernetes deployment**

---

## 📌 Table of Contents

- [Overview](#overview)  
- [Features](#features)  
- [Repository Structure](#repository-structure)  
- [Getting Started](#getting-started)  
  - Prerequisites  
  - Setup Secrets  
  - Clone & Run Manually  
  - Using CI/CD (GitHub Actions)  
- [Deployment Details](#deployment-details)   
- [Contributing](#contributing)  
- [License](#license)

---

## 🧭 Overview

This repository is intended as a boilerplate / starter kit for DevOps workflows.  
It demonstrates how to:

- Build a containerized application  
- Automate builds and image publishing with GitHub Actions  
- Deploy to Kubernetes (using manifests / Helm)  

You can clone or fork this repo, plug in your own credentials and cluster, and get a full DevOps pipeline working.

---

## ⚙ Features

- Sample web application (Python / Flask)  
- Dockerfile for containerization  
- GitHub Actions workflow: build → push → deploy  
- Kubernetes manifests: Deployment, Service, Ingress  
- Clear folder structure and documentation  

---

## 🗂 Repository Structure

```
.
├── .github/
│   └── workflows/
│       └── ci-cd.yml            # CI/CD pipeline config
├── app/
│   ├── app.py                   # Sample Flask app
│   └── requirements.txt         # Python dependencies
├── manifests/                    # Kubernetes manifest files
│   ├── deployment.yaml
│   ├── service.yaml
│   └── ingress.yaml             # (optional)
├── Dockerfile                    # To containerize the app
├── README.md
└── LICENSE
```

- **`.github/workflows/ci-cd.yml`**: Defines build & deployment pipeline  
- **`app/`**: The sample application code  
- **`manifests/`**: Kubernetes objects to deploy the app  
- **`Dockerfile`**: How to build the app container  

---

## 🏁 Getting Started

### Prerequisites

- Docker  
- kubectl  
- A running Kubernetes cluster (local or cloud)  
- A container registry (e.g. Docker Hub)  

### Setup Secrets

Before the GitHub Actions pipeline will work, set up the following repository secrets:

| Secret Name         | Description                                  |
|---------------------|----------------------------------------------|
| `DOCKER_USERNAME`   | Your Docker Hub username                      |
| `DOCKER_PASSWORD`   | Your Docker Hub password or access token      |
| `KUBE_CONFIG`       | Contents of your `~/.kube/config` or cluster kubeconfig |

> **Note:** You should configure all the secrets in your own repository settings.

### Clone & Run Locally (manual)

You can test locally without using GitHub Actions:

```bash
git clone https://github.com/subinsabu390/devops-starter-kit.git
cd devops-starter-kit

# Build the Docker image
docker build -t sample-app:latest .

# Run it locally
docker run -p 5000:5000 sample-app:latest
```

Then, if you have `kubectl` access to a cluster:

```bash
kubectl apply -f manifests/
```

Your app should be deployed to Kubernetes.

### Using CI/CD (GitHub Actions)

1. Fork this repository (or clone & push to your own).  
2. Add the required secrets (`DOCKER_USERNAME`, `DOCKER_PASSWORD`, `KUBE_CONFIG`).  
3. Push to `main` branch (or open PR) — the workflow will build, push, and deploy automatically.  
4. Check pipeline runs in **Actions** tab.  

---

## 📦 Deployment Details

- The **build step** uses Docker to containerize `app/`  
- The **push step** uploads to your registry with tag `latest` (and optionally commit SHA)  
- The **deploy step** uses `kubectl apply -f manifests/` to update your cluster  

By default, the manifests refer to the `:latest` image tag — you can modify them or use versioned tagging in future enhancements.

---

## 🤝 Contributing

Contributions are welcome!  
If you find bugs, have suggestions, or want to extend the project, feel free to open issues or submit pull requests.

When contributing, please:

- Write clear and meaningful commit messages  
- Update documentation if applicable  
- Follow existing code structure and style  

You can also **introduce new features** to this project — for example, adding:
- Monitoring and observability (Prometheus, Grafana)  
- Helm chart support  
- Secrets management  
- Logging or alerting integrations  
- CI/CD enhancements

This project is designed to be a flexible starting point for DevOps workflows, so contributions that expand its functionality are highly encouraged!
 

---

## 📝 License

This project is licensed under the **Apache-2.0 License**. See `LICENSE` for details.
