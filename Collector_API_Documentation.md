
# Collector API – Documentation

## Overview
The Collector API is a lightweight Python FastAPI application built as Phase 1 of a data collection and monitoring pipeline.

The current focus is to:
- Provide a health check endpoint to verify that the API is running
- Collect public data from an external source (JSONPlaceholder)
- Return that data as JSON for validation and testing

Later phases will:
- Store data in a database (Postgres/Mongo)
- Integrate with Gloo AI to analyze content and detect bots/spam
- Trigger notifications or actions based on analysis results

## Project Structure
```
C:\API\collector-api\
│
├── app.py          # FastAPI application code
└── Dockerfile      # Docker build instructions
```

## API Endpoints

### 1️⃣ GET /
**Purpose:** Quick health check endpoint.  
**Response Example:**
```json
{"status": "Collector API is running!"}
```

### 2️⃣ GET /collect
**Purpose:** Pulls public test data from JSONPlaceholder.

- Fetches 100 dummy posts from https://jsonplaceholder.typicode.com/posts
- Returns the first 5 posts for demo/testing

**Response Example:**
```json
{
  "count": 100,
  "data": [
    { "userId": 1, "id": 1, "title": "sunt aut facere...", "body": "quia et suscipit..." },
    ...
  ]
}
```

## Running Locally

**Install Dependencies:**
```powershell
pip install fastapi uvicorn requests
```

**Start the API:**
```powershell
cd C:\API\collector-api
uvicorn app:app --host 0.0.0.0 --port 8080
```

**Test the API:**
- PowerShell: `Invoke-RestMethod http://localhost:8080/` → Returns `{"status":"Collector API is running!"}`
- Browser: Visit `http://localhost:8080/docs` → see Swagger UI for testing endpoints.

## Dockerization

**Dockerfile:**
```dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY app.py /app
RUN pip install --no-cache-dir fastapi uvicorn requests
EXPOSE 8080
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8080"]
```

**Build Image Directly into Minikube:**
```powershell
minikube image build -t collector-api:latest .
```

## Kubernetes & Gloo Gateway Integration (Planned)
1. Kubernetes Deployment: Runs collector-api:latest as pods inside Minikube.  
2. Kubernetes Service: Exposes the pods internally at port 8080.  
3. Gloo VirtualService: Routes external traffic via Gloo Gateway.

## Future Roadmap
- Phase 1 (now): API works and fetches sample data.  
- Phase 2: Add DB integration (Postgres/Mongo) and store collected data.  
- Phase 3: Integrate Gloo AI for bot/spam detection.  
- Phase 4: Notifications, automation, and scaling.

## Summary
- FastAPI app built (app.py)  
- Endpoints working (`/`, `/collect`)  
- Dockerfile created for containerization  
- Ready for Kubernetes deployment into Minikube  
- Gloo Gateway integration planned for routing external traffic  

This Collector API is the foundation for a scalable system that will collect, process, and analyze public data through Gloo Gateway + Gloo AI.
