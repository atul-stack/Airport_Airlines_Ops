# Airport_Airlines_Ops
A fully containerized 3-tier airline airport operations system built using Java Spring Boot microservices, React frontend, and deployed on AWS with Kubernetes and Terraform.

Awesome! Here's a complete, professional-level `README.md` structure tailored for your **Airline Airport Operations Microservices Project** — with **diagrams, setup steps, tech stack, and deployment guide**.

---

## ✈️ Airline Airport Operations – Microservices on AWS

A cloud-native, microservices-based airline airport operations platform built using Java Spring Boot and React, deployed on AWS via EKS and managed entirely through Terraform.

---

### 🗺️ Architecture Diagram

```
[ React Frontend ] <---> [ API Gateway ] <---> [ Microservices ]
                                       |
   ------------------------------------------------------------
   | Booking | Check-in | Boarding | Luggage | Lounge | Cargo |
   ------------------------------------------------------------
        |         |          |         |         |      |
      RDS      Lambda     Vault     S3/ELK    RDS     ELK
        |         |                    |
     Logging + Monitoring         Event-driven
        |
     Kibana Dashboard
```

---

## 🧰 Tech Stack

| Layer             | Tech                                  |
|-------------------|----------------------------------------|
| Backend           | Java + Spring Boot (Microservices)     |
| Frontend          | React                                  |
| Infra             | AWS (EC2, EKS, RDS, Lambda, S3)        |
| IaC               | Terraform                              |
| CI/CD             | GitHub Actions                         |
| Containerization  | Docker                                 |
| Orchestration     | Kubernetes                             |
| Secrets           | HashiCorp Vault                        |
| Observability     | ELK Stack + Kibana                     |
| Event Trigger     | AWS Lambda (on Check-in)               |

---

## 🧩 Microservices Overview

| Service     | Description                              |
|-------------|------------------------------------------|
| Booking     | Search, book, cancel flights             |
| Check-in    | Passenger check-in, triggers AWS Lambda  |
| Boarding    | Generates boarding passes                |
| Luggage     | Baggage handling + tracking              |
| Lounge      | Access eligibility & reservation         |
| Cargo       | Cargo shipment tracking                  |

---

## 🚀 How to Run This Project

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/airline-airport-ops.git
cd airline-airport-ops
```

---

### 2. Deploy Infrastructure with Terraform

```bash
cd terraform
terraform init
terraform apply
```

This will:
- Set up AWS VPC, EC2 instances (in private subnet)
- Create EKS cluster
- Set up IAM roles, S3 buckets, RDS, Vault, ELK, Lambda
- Output kubeconfig and credentials

---

### 3. Build & Push Docker Images

```bash
cd backend/booking-service
docker build -t your-dockerhub/booking-service .
docker push your-dockerhub/booking-service

# Repeat for other services...
```

---

### 4. Deploy to Kubernetes

```bash
kubectl apply -f k8s/booking-deployment.yaml
kubectl apply -f k8s/frontend-deployment.yaml
# and so on...
```

---

### 5. Access the Frontend

Once the LoadBalancer service is up:

```
http://<load-balancer-ip>
```

---

## 🔒 Secrets & Configs

- Secrets are managed using **HCP Vault**
- Configs are injected via Kubernetes Secrets and Vault integrations

---

## 📈 Observability

- Logs are sent to **Elasticsearch** via Logstash
- Visualized in **Kibana Dashboard**

---

## ⚡ Event-Driven Triggers

- On successful **Check-in**, a Lambda function is triggered via SNS to:
  - Send email confirmation
  - Trigger boarding preparation
  - Start baggage tracking workflow

---

## 🧪 CI/CD with GitHub Actions

- Auto-build and deploy on `push` to `main`
- Separate pipelines for backend, frontend, Terraform

```yaml
# .github/workflows/backend.yml
on: [push]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Build Docker
        run: docker build -t booking-service .
      - name: Push Docker
        run: docker push booking-service
      - name: Deploy to K8s
        run: kubectl apply -f k8s/booking-deployment.yaml
```

---

## 📂 Folder Structure

```
.
├── backend/
│   ├── booking-service/
│   ├── checkin-service/
│   └── ...
├── frontend/
│   ├── booking-frontend/
│   └── ...
├── terraform/
├── k8s/
├── vault/
├── lambda/
└── .github/
```

---

## 📜 License

[MIT](LICENSE)

