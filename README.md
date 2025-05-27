from pathlib import Path

readme_en_content = """\
# Flask + Redis Application with Docker and Kubernetes

This project demonstrates a simple web application using Flask and Redis, deployed first via Docker and then on Kubernetes.

## 🔧 Technologies Used

- Python (Flask)
- Redis
- Docker
- Kubernetes (Minikube or Docker Desktop)

---

## 🐳 Docker Deployment

### 1. Build Docker Image

```bash
docker build -t flask-redis-app .
```

### 2. Create Docker Network

```bash
docker network create demo-net
```

### 3. Run Redis Container

```bash
docker run -d --name redis --network demo-net redis
```

### 4. Run Flask App Container

If port 5000 is occupied, use another one (e.g., 5001):

```bash
docker run -d -p 5001:5000 --name flask-app --network demo-net flask-redis-app
```

### 5. Test

Go to [http://localhost:5001](http://localhost:5001) in your browser.

---

## ☸️ Kubernetes Deployment

### 1. Required YAML Files

- `flask-deployment.yaml` — Deployment for Flask App  
- `flask-service.yaml` — Service for Flask App  
- `redis-deployment.yaml` — Deployment for Redis  
- `redis-service.yaml` — Service for Redis  

### 2. Apply YAML Files

```bash
kubectl apply -f redis-deployment.yaml
kubectl apply -f redis-service.yaml
kubectl apply -f flask-deployment.yaml
kubectl apply -f flask-service.yaml
```

### 3. Check Services

```bash
kubectl get svc
```

You should see a `flask-service` of type `LoadBalancer`.

### 4. Port Forwarding

Forward to a local port:

```bash
kubectl port-forward service/flask-service 5001:80
```

### 5. Test

Go to [http://localhost:5001](http://localhost:5001) in your browser. You should see:

```
Hello! This page has been visited X times.
```

---

## 📁 Folder Structure

```
.
├── app.py
├── Dockerfile
├── requirements.txt
├── flask-deployment.yaml
├── flask-service.yaml
├── redis-deployment.yaml
└── redis-service.yaml
```

---

## ✅ To Do

- [ ] Add Helm chart support  
- [ ] Integrate with CI/CD pipeline  
- [ ] Add Kubernetes ingress  
"""

# Write to README.en.md
readme_en_path = Path("README.en.md")
readme_en_path.write_text(readme_en_content)

"README.en.md file has been created."
