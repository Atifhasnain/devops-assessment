# DevOps Assessment: WordPress Deployment with Docker, CI/CD, Logging & Monitoring

## 🎯 Objective

Deploy and secure a WordPress application on Ubuntu VM using Docker, implement CI/CD, set up logging & monitoring, and ensure security best practices.

---

## 🛠️ Prerequisites

Before you begin, ensure the following are installed or configured:

* Ubuntu 24.04 server access (VM or physical)
* Docker & Docker Compose installed on the VM
* Docker Hub account for image registry
* GitHub repository with the project code
* Domain name configured (for SSL)
* SSH access to the VM with proper keys
* SSH key or Deploy kye should be added for pushing changes

---

## ⚡ Quick Setup Instructions

### 1. Clone the Repository

```bash
git clone git@github.com:Atifhasnain/devops-assessment.git
cd devops-assessment
```

### 2. Docker Deployment

* The application is containerized using **Docker Compose**.
* Build and run containers locally (optional):

```bash
cd docker
docker compose up -d --build
```

* Exposed services:

  * WordPress: `9000` (internal)
  * NGINX: `80` & `443`
  * Prometheus: `9090`
  * Grafana: `3000`
  * Loki: `3100`
  * Node Exporter: `9100`
  * cAdvisor: `8080`

### 3. CI/CD Pipeline

* GitHub Actions automatically builds, tests, and deploys the application on every push to `main`.
* Workflow: `.github/workflows/deploy.yml`

  1. Dockerfile for customized WordPress image and security tweaks
  2. Build Docker images for WordPress, DB, NGINX, Monitoring and Logging services.
  3. Push images to Docker Hub.
  4. Deploy updates to the remote VM via SSH.

### 4. Logging

* **Loki + Promtail + Grafana** stack used for centralized logging.
* Logs collected:

  * Host system logs: `/var/log/*log`
  * Docker container logs
* Loki accessible at port `3100`
* Promtail handles log shipping to Loki
* Grafana visualizes logs

### 5. Monitoring

* **Prometheus** monitors VM and container metrics.
* Metrics collected:

  * CPU, memory, disk usage
  * Container metrics via cAdvisor
  * Node metrics via Node Exporter
* Grafana visualizes monitoring dashboards:

  * Prometheus data source: `http://prometheus:9090`
  * Loki data source: `http://loki:3100`
* Access Grafana on port `3000` (`admin/admin` credentials)

### 6. Security & Reverse Proxy

* NGINX used as a reverse proxy with **Let’s Encrypt SSL certificates**
* Security best practices applied:

  * Containers run as non-root user where possible
  * Only necessary ports exposed
  * SSL parameters configured (`ssl_params.conf`)
  * HTTP → HTTPS redirection
  * HTTP headers for security: HSTS, X-Frame-Options, X-Content-Type-Options
  * Firewall rules recommended (UFW)

---

## 🚀 Deployment Steps on VM

1. Copy repository to VM:

```bash
git clone git@github.com:Atifhasnain/devops-assessment.git
cd devops-assessment
```

2. Ensure Docker & Docker Compose installed:

```bash
sudo apt update && sudo apt install docker.io docker-compose -y
```

3. Pull and run containers via GitHub Actions or manually:

```bash
docker compose pull
docker compose up -d --remove-orphans
```

4. Access application:

* WordPress: `https://<your-domain>` or `http://<vm-ip>`
* Grafana: `https://<your-domain>:3000`
* Prometheus: `https://<your-domain>:9090`

---

## 📌 Additional Notes

* **Volumes**:

  * WordPress: `wordpress_data`
  * DB: `db_data`
  * Grafana: `grafana_data`
* **Networks**:

  * Internal bridge network `internal` for container communication
* **SSH Deployment**:

  * GitHub Actions workflow handles secure SSH deployment
  * Private key stored in GitHub secrets

---

## ✅ Deliverables

1. **Application running on VM** accessible via HTTPS.
2. **Logging & Monitoring dashboards** in Grafana.
3. **CI/CD pipeline** for automated deployments.
4. **Documentation** with setup instructions (this README).
