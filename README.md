# Project Ramadhan - API Muslim Indonesia

Proyek ini adalah API untuk menyediakan data terkait kehidupan muslim di Indonesia, termasuk jadwal sholat, doa, dan informasi kota.

## Fitur

- **Jadwal Sholat**: Mendapatkan jadwal sholat harian atau berdasarkan tanggal untuk berbagai kota di Indonesia.
- **Doa**: Koleksi doa-doa islam dengan kemampuan mendapatkan doa acak atau berdasarkan ID.
- **Kota**: Daftar kota yang tersedia untuk data jadwal sholat.
- **Autentikasi**: Sistem login dan registrasi dengan JWT token.
- **API Key**: Generate API key untuk akses protected endpoints.

## Teknologi

- **Backend**: Go (Gin framework)
- **Database**: MySQL
- **Cache**: Redis
- **Message Queue**: RabbitMQ
- **Email Worker**: Go worker untuk mengirim email
- **Scraper**: Python script untuk scraping data jadwal sholat
- **Container**: Docker & Docker Compose

## Prasyarat

- Docker
- Docker Compose
- Git

## Instalasi

1. **Clone repository**:

   ```bash
   git clone https://github.com/OctavianoRyan25/muslimIN-api.git
   cd project-ramadhan
   ```

2. **Siapkan environment file**:
   Buat file `.env` di root directory dengan konfigurasi berikut:

   ```env
   DB_HOST=mysql_db
   DB_PORT=3306
   DB_USER=root
   DB_PASSWORD=123456
   DB_NAME=go_multi_api

   REDIS_HOST=redis_cache
   REDIS_PORT=6379

   RABBITMQ_HOST=rabbitmq_mq
   RABBITMQ_PORT=5672
   RABBITMQ_USER=guest
   RABBITMQ_PASSWORD=guest

   JWT_SECRET=your_jwt_secret_here
   ```

3. **Jalankan aplikasi**:

   ```bash
   docker-compose up --build
   ```

   Aplikasi akan berjalan di:
   - API: http://localhost:8080
   - RabbitMQ Management: http://localhost:15672 (guest/guest)
   - MySQL: localhost:3306

## Penggunaan

### Health Check

```bash
curl http://localhost:8080/api/health
```

### Registrasi

```bash
curl -X POST http://localhost:8080/api/register \
  -H "Content-Type: application/json" \
  -d '{"username": "user", "password": "pass"}'
```

### Login

```bash
curl -X POST http://localhost:8080/api/login \
  -H "Content-Type: application/json" \
  -d '{"username": "user", "password": "pass"}'
```

Response akan memberikan JWT token. Gunakan token ini untuk endpoint protected.

### Generate API Key

```bash
curl -X POST http://localhost:8080/api/generate-api-key \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

### Mendapatkan Daftar Kota

```bash
curl http://localhost:8080/api/city
```

### Mendapatkan Jadwal Sholat Hari Ini

```bash
curl "http://localhost:8080/api/jadwal-sholat-today/jakarta"
```

### Mendapatkan Jadwal Sholat Berdasarkan Tanggal

```bash
curl "http://localhost:8080/api/jadwal-sholat?city=jakarta&date=2024-03-16"
```

### Mendapatkan Semua Doa

```bash
curl http://localhost:8080/api/doa
```

### Mendapatkan Doa Acak

```bash
curl http://localhost:8080/api/doa/random
```

### Mendapatkan Doa Berdasarkan ID

```bash
curl http://localhost:8080/api/doa/1
```

## Struktur Proyek

```
project-ramadhan/
├── docker-compose.yml
├── .env
├── data/
│   └── adzan/
│       └── [kota]/
├── go/
│   ├── Dockerfile
│   ├── go.mod
│   ├── cmd/
│   │   ├── api/
│   │   └── worker/
│   └── internal/
├── python/
│   ├── Dockerfile
│   ├── parser.py
│   └── requirements.txt
└── README.md
```

## Development

### Menjalankan Parser Python

Untuk mengupdate data jadwal sholat:

```bash
cd python
python3 parser.py
```

Atau menggunakan Docker:

```bash
docker-compose run --rm scraper
```

### Menjalankan Worker Go

Worker untuk memproses background tasks seperti pengiriman email:

Worker akan berjalan otomatis dalam container `mail-worker`.

## Kontribusi

1. Fork repository
2. Buat branch fitur baru (`git checkout -b feature/AmazingFeature`)
3. Commit perubahan (`git commit -m 'Add some AmazingFeature'`)
4. Push ke branch (`git push origin feature/AmazingFeature`)
5. Buat Pull Request

## Lisensi

Distributed under the MIT License. See `LICENSE` for more information.

## Kontak

Octaviano Ryan - [@your_twitter](https://twitter.com/your_twitter) - email@example.com

Project Link: [https://github.com/OctavianoRyan25/muslimIN-api](https://github.com/OctavianoRyan25/muslimIN-api)
