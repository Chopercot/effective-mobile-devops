# Effective Mobile - DevOps Test Project

A small demonstration project showcasing a **Python HTTP server (backend)** running behind an **Nginx reverse proxy**, both deployed inside Docker containers.

The project demonstrates core containerization best practices:

- Utilizing `docker-compose`
- Service separation (1 process = 1 container)
- Using a `.env` file for configuration
- Isolated Docker network
- Clean, minimal backend image

---

# Architecture

```

        Browser / Client
               │
               │ HTTP
               ▼
     ┌────────────┐
     │   Nginx    │
     │ (reverse   │
     │   proxy)   │
     └─────┬──────┘
           │
           │ proxy_pass
           ▼
     ┌────────────┐
     │  Backend   │
     │  Python    │
     │ HTTP server│
     │   :8080    │
     └────────────┘     
```

**Nginx** accepts HTTP requests and proxies them to the **application**.

All services run within an **isolated Docker network**.

---

# Tech Stack

* Docker
* Docker Compose
* Nginx
* Python
* Linux

---

# Project Structure

```

effective-mobile-devops/
├── backend/                     # Backend service (Python HTTP server)
│   ├── Dockerfile               # Dockerfile for the backend
│   └── app.py                   # Main application code
│
├── nginx/                       # Nginx (reverse proxy)
│   └── nginx.conf               # Nginx configuration file
│
├── .dockerignore                # Files excluded from the Docker image
├── .env                         # Environment variables for docker-compose
├── docker-compose.yml           # Configuration to spin up all containers
├── README.md                    # Instructions, verification, and architecture overview
|
└── .gitignore                   # Git ignored files

```
---

# Environment Variables

`.env` file:

```
NGINX_PORT=8080
```

---

# Getting Started

### 1. Clone the repository
```Bash
git clone <repo_url>
cd project
```

### 2. Start the containers
```Bash
docker compose up --build
```

---

# Verification
Verify using curl:

```Bash
curl http://localhost:8080
```
Expected response:

```Bash
Hello from Effective Mobile!
```
---

# Useful Commands

View running containers:

```Bash
docker ps
```

View logs:

```Bash
docker compose logs
```

Stop containers:

```Bash
docker compose down
```

# Key Features & Implementation Details

✔ Nginx acts as a **reverse proxy**
✔ The application runs in a separate container
✔ Containers are joined in **an isolated Docker network**
✔ Configurations are managed **via environment variables in a .env file**
✔ Each container runs a **single process**
✔ The backend container runs under a non-root user
✔ The backend service is not directly accessible from the outside
✔ Access to the application is routed exclusively through Nginx
