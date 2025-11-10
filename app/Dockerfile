# === Stage 1: build dependencies ===
FROM python:3.12-slim AS builder

WORKDIR /app

# install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential gcc \
 && rm -rf /var/lib/apt/lists/*

# upgrade pip and install deps
COPY requirements.txt .
RUN pip install --upgrade pip && pip install --no-cache-dir -r requirements.txt

# === Stage 2: runtime image ===
FROM python:3.12-slim

WORKDIR /app

# copy installed libs from builder
COPY --from=builder /usr/local /usr/local

# copy only necessary app files
COPY . .

# environment configuration
ENV PYTHONUNBUFFERED=1 \
    FLASK_APP=flaskr \
    FLASK_RUN_HOST=0.0.0.0 \
    FLASK_DEBUG=0

EXPOSE 5000

# simple runtime healthcheck
HEALTHCHECK CMD wget --quiet --tries=1 --spider http://localhost:5000/health || exit 1

ENV FLASK_APP=flaskr \
    FLASK_RUN_HOST=0.0.0.0 \
    FLASK_RUN_PORT=5000 \
    FLASK_DEBUG=0 \
    PYTHONUNBUFFERED=1

CMD ["flask", "run", "--host=0.0.0.0"]
