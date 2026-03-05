FROM python:3.11-slim

# Install library sistem yang dibutuhkan oleh lxml (C compiler & libxml)
RUN apt-get update && apt-get install -y \
    gcc \
    libxml2-dev \
    libxslt-dev \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Copy requirements terlebih dahulu untuk caching layer
# Kita akan membuat file requirements.txt secara otomatis di bawah
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy source code (parser.py)
COPY . .

# Buat direktori untuk hasil output agar tidak error saat penulisan file
# Sesuai script Anda: ../data/adzan/ (relatif terhadap script di /app)
RUN mkdir -p /data/adzan

# Environment variables default (bisa diubah saat running container)
ENV JWO_MONTH=""
ENV JWO_YEAR=""

# Jalankan script
CMD ["python", "parser.py"]