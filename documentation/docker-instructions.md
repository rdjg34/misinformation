# Docker Setup Instructions

## Overview

This project uses a single `Dockerfile` to build both the frontend (Streamlit) and backend (FastAPI) services. Orchestration between the two is handled by `docker-compose.yml`, which overrides the default entrypoint for the backend service at runtime.

---

## Project Structure

```
COLX_523_misinformation/
├── app/
│   ├── data/
│   ├── testing/
│   ├── whoosh_index/
│   ├── be_fast.py                  # FastAPI backend
│   ├── be_search.py                # Search backend logic
│   ├── docker-compose.yml
│   ├── Dockerfile
│   ├── linguistic_markers_app.py   # Streamlit frontend
│   ├── requirements.txt
│   ├── styles.css
│   └── templates.py
├── data/
├── documentation/
├── img/
├── reports/
├── src/
├── weekly_minutes/
├── environment.yml
├── LICENSE
├── linguistic_markers_app.tar
└── README.md
```

---

## How It Works

**`Dockerfile`** builds a single image based on `python:3.12-slim`. By default, its entrypoint runs the Streamlit app on port `8501`.

**`docker-compose.yml`** spins up two services from that same image:

| Service | Port | Description |
|---|---|---|
| `frontend` | `8501` | Runs the Streamlit app (uses the default Dockerfile entrypoint) |
| `backend` | `8000` | Runs the FastAPI app (overrides the entrypoint to use `uvicorn`) |

The `frontend` service is configured with a `BACKEND_URL` environment variable pointing to the backend container, and waits for the backend to start via `depends_on`.

---

## Running the App

> **Prerequisites:** Docker Desktop must be installed and **open and running** before proceeding — `docker-compose` requires the Docker daemon to be active. ([Get Docker Desktop](https://docs.docker.com/get-docker/))

No Python environment or dependency installation is required — everything runs inside the containers.

**If you've cloned the repo**, navigate to the `app` directory:

```bash
cd app
```

**If you're starting from the `.tar` archive**, download `linguistic_markers_app.tar` from the repository root, extract it, and navigate into the `app` directory:

```bash
tar -xvf linguistic_markers_app.tar
cd app
```

**Either way**, build and start the services:

```bash
docker-compose up --build
```

Once running, open your browser to:

- **Frontend (Streamlit):** http://localhost:8501
- **Backend (FastAPI):** http://localhost:8000

To stop the services:

```bash
docker-compose down
```
---

## Things to Try

Once the app is running, here are a few things worth exploring:

- **AI vs. human disagreements** — can you find an item where the AI (Gemini) and human annotations don't match? Enable *Show AI (Gemini) annotations* in the search bar to compare side by side.
- **Tag density** — what's the most tags a single annotation has?
- **Empty tag results** — note that some annotated items had no content that fell into any tag category, so not every result will have tags.

---

## Noteworthy Mentions

- **Restrictions:** No notable restrictions found.
- **Considerations:** Our team chose not to include the classification labels (misinformation vs. fact) to prioritize human annotation insights. 
