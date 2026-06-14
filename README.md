
# LogSense AI — Hybrid Log Classification

LogSense AI is a hybrid log classification project that combines rule-based, classical ML, and LLM-powered techniques to classify log messages into categories. The repository contains code for training, inference, and a small FastAPI service for serving the classifier.

Why this approach
- Lightweight and deterministic handling for simple, repetitive patterns (regex)
- Fast embedding + classifier pipeline for supervised scenarios (Sentence Transformers + Logistic Regression)
- LLM-based fallbacks for ambiguous or low-data scenarios

--

## Quickstart

Requirements
- Python 3.8+ (a virtual environment is recommended)

Install dependencies:

```bash
pip install -r requirements.txt
```

Start the API server (development mode):

```bash
uvicorn server:app --reload
```

Open the API docs:
- http://127.0.0.1:8000/docs

--

## Usage

The service accepts a CSV file of logs and returns a CSV with predicted labels.

Expected input CSV columns:
- `source` — origin of the log (optional)
- `log_message` — the raw log text to classify

Example workflow:
1. POST the CSV to the classification endpoint (see `/docs` for exact path).
2. Download the result CSV with the added `target_label` column.

--

## Project Structure

- `classify.py` — main classification orchestration
- `processor_regex.py` — rule-based classifiers
- `processor_bert.py` — embedding + logistic regression pipeline
- `processor_llm.py` — LLM integration / fallback
- `server.py` — FastAPI app and endpoints
- `requirements.txt` — Python dependencies
- `models/` — trained model artifacts (not tracked by default)
- `resources/` — supporting files (images, sample CSVs)
- `training/` — notebooks and training scripts
