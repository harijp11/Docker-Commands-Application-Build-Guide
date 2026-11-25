# Docker-Commands-Application-Build-Guide

## 1. Docker Installation Verification

```powershell
docker --version
docker compose version
docker info
docker run hello-world
```

## 2. Basic Docker Commands

### Images

```powershell
# Build image
docker build -t my-app:v1 .

# List images
docker images

# Pull image
docker pull nginx

# Remove image
docker rmi my-app:v1

# Build without cache
docker build --no-cache -t my-app:v1 .
```

### Containers

```powershell
# Create and start container
docker run -d -p 8080:8080 --name my-container my-app:v1

# List running containers
docker ps

# List all containers
docker ps -a

# Stop container
docker stop my-container

# Start container
docker start my-container

# Restart container
docker restart my-container

# Remove container
docker rm my-container

# View logs
docker logs my-container

# Follow logs
docker logs -f my-container

# Enter container
docker exec -it my-container sh
```

## 3. Port Mapping

```powershell
docker run -d -p 8080:8080 my-app:v1
```

Format:

```text
-p HOST_PORT:CONTAINER_PORT
```

## 4. Docker Volume Commands

```powershell
docker volume create my-volume
docker volume ls
docker volume inspect my-volume
docker volume rm my-volume
```

## 5. Docker Network Commands

```powershell
docker network create my-network
docker network ls
docker network inspect my-network
docker network rm my-network
```

## 6. Docker Compose Commands

```powershell
# Build all images
docker compose build

# Build one service image
docker compose build user-service

# Create containers
docker compose create

# Start services
docker compose start

# Start all services
docker compose up -d

# Build images and start services
docker compose up --build -d

# Build and start one service
docker compose up --build -d user-service

# Stop services
docker compose stop

# Stop and remove containers
docker compose down

# Restart one service
docker compose restart user-service

# Force recreate one service
docker compose up -d --force-recreate user-service

# Check running services
docker compose ps

# View all logs
docker compose logs

# Follow all logs
docker compose logs -f

# View specific service logs
docker compose logs -f user-service

# View latest 50 log lines
docker compose logs --tail=50 user-service

# Validate Compose configuration
docker compose config
```

---

# 7. Build and Run Go Microservices Application

## Project Structure

```text
API/
│
├── docker-compose.yml
├── go.mod
├── go.sum
│
├── shared/
│
├── auth-service/
│   ├── Dockerfile
│   └── cmd/
│
├── user-service/
│   ├── Dockerfile
│   └── cmd/
│
└── api-gateway/
    ├── Dockerfile
    └── cmd/
```

## Step 1: Navigate to Project Directory

```powershell
cd C:\Users\harij\WorkShop\Go\Deployer\API
```

## Step 2: Build Individual Service Images

```powershell
docker compose build auth-service
docker compose build user-service
docker compose build api-gateway
```

## Step 3: Create Containers

```powershell
docker compose create
```

## Step 4: Start All Containers

```powershell
docker compose start
```

Alternatively, create and start everything in one command:

```powershell
docker compose up -d
```

## Step 5: Check Container Status

```powershell
docker compose ps
```

## Step 6: Check Individual Service Logs

```powershell
docker compose logs -f api-gateway
docker compose logs -f auth-service
docker compose logs -f user-service
```

## Step 7: View All Service Logs

```powershell
docker compose logs -f --tail=50
```

---

# 8. Updating Application Code

### Step 1: Modify Go Source Code

Make changes inside the required service.

### Step 2: Build Updated Image and Recreate Container

```powershell
docker compose up --build -d user-service
```

For other services:

```powershell
docker compose up --build -d auth-service
docker compose up --build -d api-gateway
```

### Step 3: Verify Updated Container

```powershell
docker compose ps
docker compose logs --tail=50 user-service
```

---

# 9. Stop and Remove Application Containers

```powershell
# Stop all services
docker compose stop

# Stop and remove containers and Compose network
docker compose down
```

---

# 10. Docker Cleanup Commands

```powershell
# Remove stopped containers
docker container prune

# Remove unused images
docker image prune

# Remove unused networks
docker network prune

# Remove unused volumes
docker volume prune

# Remove unused Docker resources
docker system prune

# Check Docker disk usage
docker system df
```

**Warning:** Review cleanup operations before confirming. Removing unused volumes can permanently delete stored data.
