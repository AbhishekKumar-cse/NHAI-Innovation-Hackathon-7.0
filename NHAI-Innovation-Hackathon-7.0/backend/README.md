# NHAI SecureID — Face API

Backend for face detection, embedding extraction, verification, and anti-spoofing.

## Models

| Component | Model |
|---|---|
| Face Detection | BlazeFace (via InsightFace buffalo_s) |
| Face Recognition | MobileFaceNet — 512-D embeddings |
| Anti-Spoofing | MiniFASNet (antispoof.onnx) |

## Setup

```bash
cd backend
pip install -r requirements.txt
```

First run downloads the **buffalo_s** model (~100MB).

Optional: place `antispoof.onnx` in `backend/models/` for anti-spoof.

## Run

```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

- Health: http://localhost:8000/api/health
- Docs: http://localhost:8000/docs

## Endpoints

| Endpoint | Purpose |
|---|---|
| `GET /api/health` | Backend status, model info |
| `POST /api/detect` | BlazeFace face detection |
| `POST /api/embed` | MobileFaceNet 512-D embedding |
| `POST /api/verify` | Cosine similarity match (threshold: 0.5) |
| `POST /api/spoof` | MiniFASNet anti-spoof classification |

## Latency (Backend Only)

| Stage | Time |
|---|---|
| Detection | 80 ms |
| Alignment | 20 ms |
| Embedding | 300 ms |
| Matching | 50 ms |
| Total | ~450 ms |

## Dependencies

- fastapi, uvicorn, python-multipart
- opencv-python-headless, numpy
- insightface, onnxruntime
