# Docker Project

[![FastAPI CI](https://github.com/Priyu49/Docker-Project/actions/workflows/ci.yaml/badge.svg)](https://github.com/Priyu49/Docker-Project/actions/workflows/ci.yaml)

A small FastAPI application for learning Docker and GitHub Actions. It exposes a few sample endpoints and can run locally or in a Docker container.

## Features

- FastAPI application with home, about, health, and products endpoints
- Docker image based on Python 3.12
- Pytest tests using FastAPI's `TestClient`

## Project structure

```text
.
├── main.py
├── dockerfile
├── requirements.txt
├── tests/
│   └── test_main.py
└── .github/
    └── workflows/
        └── ci.yaml
```

## Run locally on Windows

Open PowerShell in the project directory and run. If `.venv` already exists and you previously saw the stale interpreter path or Pydantic import error, remove and recreate it first:

```powershell
if (Test-Path .venv) { Remove-Item -Recurse -Force .venv }
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m uvicorn main:app --reload
```

The API is available at <http://127.0.0.1:8000>. Interactive API documentation is at <http://127.0.0.1:8000/docs>.

To run the tests:

```powershell
python -m pytest tests/test_main.py -v
```

## API endpoints

| Method | Path | Description |
| --- | --- | --- |
| `GET` | `/` | Application status message |
| `GET` | `/about` | Project description |
| `GET` | `/health` | Health status |
| `GET` | `/products` | Sample product list |

## Build and run with Docker

Make sure Docker Desktop is running and its Linux engine is ready. From the project directory, build the image:

```powershell
docker build -t fastapi-app .
```

Create and start a container:

```powershell
docker run -d --name fastapi-app-container -p 8000:8000 fastapi-app
```

Open <http://localhost:8000/docs> to view the API documentation. Useful container commands:

```powershell
docker ps
docker logs fastapi-app-container
docker stop fastapi-app-container
docker rm fastapi-app-container
```

If a container with that name already exists, remove it before creating another one:

```powershell
docker rm -f fastapi-app-container
```
