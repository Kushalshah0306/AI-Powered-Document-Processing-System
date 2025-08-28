# AI-Powered Document Processing System (Prototype Scaffold)

A modular, production-ready scaffold aligned with the **AI-Powered Document Processing System** assessment. 
It includes ingestion, OCR, classification, extraction, validation, enrichment, distributed processing, API, monitoring, and deployment templates.

> This is a **working prototype scaffold** intended for rapid extension. 
> Heavy models & enterprise integrations are stubbed with clean interfaces so you can swap in your preferred services (Textract, Form Recognizer, Vertex AI, etc.).

## Quick Start (Local)

```bash
# 1) Create a virtual environment
python -m venv .venv && source .venv/bin/activate  # Windows: .venv\Scripts\activate

# 2) Install deps
pip install -r requirements.txt

# 3) Run API
uvicorn src.app:app --reload --port 8000

# 4) Try sample endpoints:
# Health
curl http://localhost:8000/health
# Process a sample local file (path as query for simplicity)
curl "http://localhost:8000/process?path=sample_docs/sample_text_invoice.txt&priority=true"
```

## Architecture (High Level)

- **FastAPI** service exposes endpoints for ingestion, processing, validation, search, and monitoring.
- **OCR Engine** interface supports pluggable OCR (Tesseract, AWS Textract, Azure Form Recognizer, Google Vision).
- **NLP** modules for classification and field extraction (transformers-ready, currently lightweight heuristic + spaCy optional).
- **Validation** rule engine supports configurable JSON rules + Python plugins.
- **Enrichment** integrates a tiny knowledge-graph (rdflib) stub.
- **Distributed Processing** via **Ray** worker for parallel execution (Spark/Dask can be added).
- **Storage** abstractions for local FS and cloud (S3/GCS/Azure) placeholders.
- **Monitoring** with Prometheus client metrics and structured logging.
- **Deployments**: Dockerfile, docker-compose, and Kubernetes manifests.

## Notes
- To use real OCR/LLM providers, implement the TODOs in `src/ocr/ocr_engine.py` and `src/nlp/*` with your keys and models.
- The system is designed for **hot-swapping** components via config in `configs/app.yaml`.

## Project Layout
```
src/
  app.py
  core/
    config.py
    logger.py
  ingestion/
    producer.py
    consumer.py
  ocr/
    ocr_engine.py
  nlp/
    classifier.py
    extractor.py
  validation/
    rules_engine.py
  enrichment/
    knowledge_graph.py
  pipeline/
    worker.py
    schemas.py
  storage/
    storage.py
  monitoring/
    metrics.py
configs/
  app.yaml
docker/
  Dockerfile
  docker-compose.yml
k8s/
  deployment.yaml
  service.yaml
sample_docs/
  sample_text_invoice.txt
tests/
  test_basic.py
scripts/
  run_local.sh
```

## License
MIT (for the scaffold). You are responsible for licenses of external models/services you integrate.
