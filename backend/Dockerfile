FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /app

# PostgreSQL runtime/build dependencies
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       libpq5 \
       gcc \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .

# Convert UTF-16 requirements.txt to UTF-8
RUN iconv -f UTF-16 -t UTF-8 requirements.txt > /tmp/requirements.txt \
    && pip install --no-cache-dir -r /tmp/requirements.txt

COPY . .

EXPOSE 80

CMD ["gunicorn", "barcode_management.wsgi:application", "--bind", "0.0.0.0:8000"]