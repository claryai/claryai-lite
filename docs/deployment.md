# Deployment Guide for Clary AI Lite

This guide provides instructions for deploying Clary AI Lite using Docker.

## Prerequisites

- Docker and Docker Compose installed
- 4GB+ RAM
- 5GB+ free disk space

## Deployment Steps

### 1. Clone the Repository

```bash
git clone https://github.com/your-org/claryai-lite.git
cd claryai-lite
```

### 2. Initialize and Update the Submodule

```bash
git submodule init
git submodule update
```

### 3. Create a `.env` File

```bash
cp core/.env.example .env
```

Edit the `.env` file to configure your deployment:

```
# API Configuration
API_PORT=8000
API_HOST=0.0.0.0
DEBUG=true
PROJECT_NAME=Clary AI Lite

# Database Configuration
DB_USER=claryai
DB_PASSWORD=your_secure_password
DB_NAME=claryai
DB_HOST=db

# Security
API_KEY_SALT=your_random_salt_string
JWT_SECRET=your_jwt_secret

# License Configuration
LICENSE_VALIDATION_ENABLED=true
LICENSE_SERVER_URL=https://api.claryai.com/license
LICENSE_CHECK_INTERVAL=24
CONTAINER_ID=your_container_id_here

# Tier Configuration
TIER=lite
LLM_INTEGRATION=false

# Web UI
WEB_PORT=3000
```

### 4. Start the Services

```bash
docker-compose up -d
```

This will start all the required services:
- Web UI on port 3000
- API on port 8000
- PostgreSQL database

### 5. Initialize the Database

```bash
docker-compose exec api python scripts/init_db.py
```

### 6. Activate the Container

When you first access the application, you'll be prompted to enter an API key. You can obtain an API key from the Clary AI website or from your account manager.

```bash
docker-compose exec api python scripts/activate_container.py --api-key YOUR_API_KEY
```

### 7. Access the Application

Open your browser and navigate to:

```
http://localhost:3000
```

## Production Deployment

For production environments, additional security and performance considerations are necessary.

### 1. Configure Production Environment Variables

Create a `.env.production` file:

```
# API Configuration
API_PORT=8000
API_HOST=0.0.0.0
DEBUG=false

# Database Configuration
DB_USER=claryai
DB_PASSWORD=your_very_secure_password
DB_NAME=claryai
DB_HOST=db

# Security
API_KEY_SALT=your_random_salt_string
JWT_SECRET=your_jwt_secret
ENABLE_RATE_LIMITING=true
RATE_LIMIT_PER_MINUTE=100

# License Configuration
LICENSE_VALIDATION_ENABLED=true
LICENSE_SERVER_URL=https://api.claryai.com/license
LICENSE_CHECK_INTERVAL=24
CONTAINER_ID=your_container_id_here

# Tier Configuration
TIER=lite
LLM_INTEGRATION=false

# Web UI
WEB_PORT=3000

# TLS/SSL
ENABLE_TLS=true
TLS_CERT_PATH=/path/to/cert.pem
TLS_KEY_PATH=/path/to/key.pem
```

### 2. Use Production Docker Compose File

Create a `docker-compose.prod.yml` file:

```yaml
version: '3'
services:
  web:
    build:
      context: ./core/web
      dockerfile: Dockerfile.prod
    ports:
      - "443:3000"
    depends_on:
      - api
    volumes:
      - ./data:/app/data
      - ./certs:/app/certs
    env_file:
      - .env.production
    restart: always

  api:
    build:
      context: ./core
      dockerfile: ../Dockerfile
    ports:
      - "8443:8000"
    volumes:
      - ./models:/app/models
      - ./data:/app/data
      - ./certs:/app/certs
    env_file:
      - .env.production
    restart: always

  db:
    image: postgres:14
    env_file:
      - .env.production
    volumes:
      - postgres_data:/var/lib/postgresql/data
    restart: always
    environment:
      - POSTGRES_USER=${DB_USER}
      - POSTGRES_PASSWORD=${DB_PASSWORD}
      - POSTGRES_DB=${DB_NAME}

volumes:
  postgres_data:
```

### 3. Start the Production Services

```bash
docker-compose -f docker-compose.prod.yml up -d
```

## Troubleshooting

### API Key and License Issues

If you encounter issues with API keys or licensing:

1. Check that your API key is valid and active
2. Verify that the container ID is correctly configured
3. Ensure that the license server URL is accessible
4. Check the API logs for error messages:
   ```bash
   docker-compose logs api
   ```

### Database Connection Issues

If the API cannot connect to the database:

1. Verify that the database container is running:
   ```bash
   docker-compose ps
   ```
2. Check the database logs:
   ```bash
   docker-compose logs db
   ```
3. Ensure that the database credentials in the `.env` file are correct

### Web UI Issues

If the web UI is not accessible:

1. Verify that the web container is running:
   ```bash
   docker-compose ps
   ```
2. Check the web logs:
   ```bash
   docker-compose logs web
   ```
3. Ensure that the API URL in the `.env` file is correct

## Backup and Restore

### Database Backup

```bash
docker-compose exec db pg_dump -U claryai claryai > backup_$(date +%Y%m%d).sql
```

### Database Restore

```bash
cat backup_YYYYMMDD.sql | docker-compose exec -T db psql -U claryai claryai
```

## Updating the Application

### 1. Pull the Latest Changes

```bash
git pull origin main
git submodule update --remote
```

### 2. Rebuild and Restart the Services

```bash
docker-compose down
docker-compose build
docker-compose up -d
```
