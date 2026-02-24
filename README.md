# DevOps Engineer Machine Test

## Objective

This project demonstrates DevOps fundamentals using a Django + React + MySQL stack.  
It includes Dockerization, environment variable management, CI pipeline setup, and Linux-based deployment steps.

---

## Technology Stack

- Backend: Django (REST API)
- Frontend: React
- Database: MySQL
- Containerization: Docker & Docker Compose
- CI: GitHub Actions
- Target Environment: Linux VPS

---

## Backend Configuration

- MySQL configuration is enabled in `settings.py`.
- Database credentials and `SECRET_KEY` are loaded from a `.env` file.
- No credentials are hardcoded.
- Environment variables are injected into the backend container using Docker Compose.
- `DEBUG=False` is supported for production.

Example `.env` (backend):

```
SECRET_KEY=your_secret_key
DEBUG=False
DB_NAME=devops_db
DB_USER=devops_user
DB_PASSWORD=devops_pass
DB_HOST=db
DB_PORT=3306
```

---

## Docker Setup

### Backend

- Python 3.11 slim image
- Installs system dependencies for MySQL
- Uses Gunicorn to serve Django
- Exposes port 8000

### Frontend

- Multi-stage build
- Node builds React app
- Nginx serves production build
- Exposes port 80

### Database

- MySQL 8.0
- Uses Docker volume for persistent data

---

## Running Locally with Docker Compose

Build and start services:

```
docker compose up -d --build
```

Services:

- Backend: http://localhost:8000
- Frontend: http://localhost:3000
- MySQL runs internally on service name `db`

Stop services:

```
docker compose down
```

---

## Docker Compose Services

- `db` → MySQL database
- `backend` → Django API (connected to db via service name)
- `frontend` → React app served via Nginx

Docker networking allows backend to connect to MySQL using:

```
DB_HOST=db
```

---

## CI Pipeline (GitHub Actions)

Steps:
1. Checkout repository
2. Setup Docker Buildx
3. Build backend image
4. Build frontend image
5. Run Django system checks

---

## Deployment on Linux VPS (SSH-Based)

1. SSH into VPS:

```
ssh user@your_server_ip
```

2. Install Docker and Docker Compose.

3. Clone repository:

```
git clone <repository_url>
cd project_directory
```

4. Create backend `.env` file with production credentials.

5. Build and run:

```
docker compose up -d --build
```

6. Open required ports (e.g., 80, 8000) in firewall/security group.