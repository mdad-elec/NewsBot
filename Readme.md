# Docker Compose Setup for n8n, PostgreSQL, MongoDB, and Qdrant

## Overview
This setup uses Docker Compose to deploy an n8n instance along with PostgreSQL, MongoDB, and Qdrant. The services are connected via a Docker network (`n8n_network`), and persistent storage is maintained using Docker volumes.

## Prerequisites
- Docker and Docker Compose installed
- `.env` file with the following environment variables:
  ```
  N8N_ENCRYPTION_KEY=your_secret_key
  ```
- A domain pointing to the server's IP
- SSL certificate configured if using HTTPS

## Services
- **n8n**: Workflow automation tool
- **PostgreSQL**: Database backend for n8n
- **MongoDB**: Used for storing News, Users
- **Qdrant**: Vector database for similarity search

## Configuration
Modify `docker-compose.yml` as needed:
- Change `N8N_HOST` to your domain
- Update database credentials
- Ensure MongoDB connection string matches your setup

## Usage
### Starting the Services
Run the following command in the root directory:
```sh
docker-compose up -d
```

### Stopping the Services
```sh
docker-compose down
```

### Checking Logs
```sh
docker-compose logs -f
```

### Accessing the n8n UI
After the services are up, open your browser and visit:
```
http://your-domain:5678
```
If SSL is set up:
```
https://your-domain.com
```

### Persistent Data
- n8n data: `n8n_data`
- PostgreSQL data: `postgres_data`
- MongoDB data: `mongodb_data`
- Qdrant storage: `qdrant_storage`

## Notes
- Ensure `mongo-init.js` is in the root directory to initialize MongoDB.
- The `depends_on` directive ensures n8n starts only after required databases are available.
- If using a reverse proxy like Nginx, update the `WEBHOOK_URL` accordingly.
