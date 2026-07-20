FROM python:3.12-slim

WORKDIR /app

# Instalam varianta CPU-only de PyTorch (fara drivere CUDA de 15 GB) + sentence-transformers si fastapi
RUN pip install --no-cache-dir torch --index-url https://download.pytorch.org/whl/cpu
RUN pip install --no-cache-dir sentence-transformers fastapi uvicorn pydantic

# Pre-descarcam modelul de AI CrossEncoder in timpul build-ului
RUN python -c "from sentence_transformers import CrossEncoder; CrossEncoder('cross-encoder/mmarco-mMiniLMv2-L12-H384-v1')"

COPY . .

EXPOSE 8002

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8002"]