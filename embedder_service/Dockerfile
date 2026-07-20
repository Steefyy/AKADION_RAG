FROM python:3.12-slim

WORKDIR /app

# Instalam varianta CPU-only de PyTorch
RUN pip install --no-cache-dir torch --index-url https://download.pytorch.org/whl/cpu

COPY pyproject.toml ./
RUN pip install --no-cache-dir . --extra-index-url https://download.pytorch.org/whl/cpu

# Pre-descarcam modelul BAAI/bge-m3 in timpul build-ului
RUN python -c "from sentence_transformers import SentenceTransformer; SentenceTransformer('BAAI/bge-m3')"

COPY fastapi_app/ fastapi_app/

EXPOSE 8001

CMD ["uvicorn", "fastapi_app.main:app", "--host", "0.0.0.0", "--port", "8001"]
