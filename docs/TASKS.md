# DevOps Assessment Tasks

## 🎯 Objective
Deploy and secure an open-source application on a provided Ubuntu VM using Docker, implement CI/CD, set up logging & monitoring, and ensure security best practices.

---

## 📝 Tasks

### 1. Application Deployment
- Choose one open-source project:
  - Ghost Blog (Node.js CMS)
  - WordPress (PHP/MySQL)
  - Whoami (lightweight app)
- Containerize the application using Docker (Docker Compose allowed).
- Deploy the containerized application on the provided Ubuntu VM.

---

### 2. CI/CD Pipeline
- Implement CI/CD using GitHub Actions (or GitLab CI if repo is on GitLab).
- On every push to `main` branch:
  1. Build the Docker image.
  2. Run a simple test (healthcheck or lint) on the built image.
- Push the Docker image to Docker Hub.
- Automatically deploy the updated container to the VM.

---

### 3. Logging
- Set up container and application logging using one of the following stacks:
  - ELK (Elasticsearch + Logstash + Kibana)
  - EFK (Elasticsearch + Fluentd + Kibana)
  - Loki + Promtail + Grafana (preferred lightweight)
- Ensure logs are accessible via a dashboard (Kibana or Grafana).

---

### 4. Monitoring
- Install Prometheus and Grafana using Docker.
- Monitor:
  - VM metrics: CPU, memory, and disk usage
  - Application/container metrics
- Provide a Grafana dashboard accessible through the browser.

---

### 5. Security
- Set up a reverse proxy using NGINX or Traefik with Let’s Encrypt SSL.
- Apply security best practices:
  - Run containers as non-root wherever possible.
  - Only expose required ports (80/443).
  - Configure UFW firewall rules to allow necessary traffic.

---

## ✅ Deliverables

1. **GitHub Repository** containing:
   - Dockerfile and docker-compose.yml
   - CI/CD pipeline configuration (.github/workflows/deploy.yml)
   - Logging and monitoring configurations
   - Documentation (README.md) with setup instructions

2. **Application Access**
   - The deployed application should be accessible at the VM IP or custom domain via HTTPS.

3. **Monitoring and Logging Dashboard**
   - Provide the Grafana/Kibana dashboard URL showing metrics and logs.

---

