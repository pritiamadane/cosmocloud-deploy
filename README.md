# cosmocloud-deploy Helm Chart

This Helm Chart deploys a simple application consisting of:
1. Backend Service
2. Frontend Service
3. Redis Database

## Chart Structure
- `Chart.yaml`: Contains metadata about the Helm Chart.
- `values.yaml`: Centralized configuration for deployments and services.
- `templates/`: Contains the deployment and service YAML templates for backend, frontend, and Redis.

## Deployment Details
### Backend
- **Image**: `shreybatra/sample-backend`
- **Replica Count**: 1
- **Environment Variable**: 
  - `REDIS_URI=redis://redis-svc:6379`
- **Service**: 
  - **Type**: ClusterIP
  - **Name**: `backend-svc`
  - **Port**: 8000

### Frontend
- **Image**: `shreybatra/sample-frontend`
- **Replica Count**: 1
- **Environment Variable**: 
  - `BACKEND_URL=http://backend-svc:8000`
- **Service**: 
  - **Type**: NodePort
  - **Name**: `frontend-svc`
  - **Port**: 5175
  - **NodePort**: 31000

### Redis
- **Image**: `redis`
- **Replica Count**: 1
- **Service**: 
  - **Type**: ClusterIP
  - **Name**: `redis-svc`
  - **Port**: 6379

## How to Deploy
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/cosmocloud-deploy.git
   cd cosmocloud-deploy
