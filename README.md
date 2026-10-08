# Bulk Certificate Generator API

A production-style FastAPI REST API that accepts recipient data in CSV/Excel format and generates individual PDF certificates in bulk.

## Features

- FastAPI REST API
- CSV/XLSX/XLS input
- Pydantic validation
- SQLAlchemy + SQLite persistence
- Unique certificate IDs
- PDF generation with ReportLab
- Individual certificate download
- Bulk ZIP download
- Delete certificate
- Automatic Swagger/OpenAPI docs
- Unit/API tests
- Docker support
- GitHub Actions CI
- Modular service-oriented structure

## Project Structure

```text
Bulk-CertificateAPI/
├── app/
│   ├── api/
│   ├── database/
│   ├── models/
│   ├── schemas/
│   ├── services/
│   └── main.py
├── docs/
├── sample_data/
├── templates/
├── tests/
├── generated/
├── .github/workflows/ci.yml
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
└── README.md
```

## Run Locally

### 1. Create environment

```bash
python -m venv .venv
```

Windows:

```bash
.venv\Scripts\activate
```

Linux/macOS:

```bash
source .venv/bin/activate
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Start API

```bash
uvicorn app.main:app --reload
```

Open:

- Swagger: http://127.0.0.1:8000/docs
- ReDoc: http://127.0.0.1:8000/redoc
- Health: http://127.0.0.1:8000/health

## Generate Certificates

Use `sample_data/recipients.csv` with:

```text
name,email,course,date
Ashok Patil,ashok@example.com,Python FastAPI Development,2026-10-01
```

In Swagger:

1. Open `POST /api/v1/certificates/bulk`
2. Click **Try it out**
3. Upload the CSV
4. Execute
5. PDFs are generated in `generated/`

Then use the returned certificate ID with the download endpoint.

## Example cURL

```bash
curl -X POST "http://127.0.0.1:8000/api/v1/certificates/bulk"   -H "accept: application/json"   -H "Content-Type: multipart/form-data"   -F "file=@sample_data/recipients.csv"
```

## Run Tests

```bash
pytest
```

## Docker

```bash
docker compose up --build
```

## API

See `docs/API.md`.

## Database

See `docs/DATABASE.md`.

## Design Decisions

See `docs/DESIGN_DECISIONS.md`.

## Debugging

See `docs/DEBUGGING.md`.

## Future Improvements

- Background jobs with Celery/RQ
- PostgreSQL for production
- Authentication and role-based access
- Email certificate delivery
- Configurable template text coordinates
- Certificate verification endpoint/QR code
- Cloud object storage
- Pagination and filtering
- Structured logging and monitoring

## Interview Explanation

The API follows a layered architecture. FastAPI handles HTTP requests, Pydantic validates input, the service layer performs certificate generation, ReportLab creates PDFs, and SQLAlchemy stores certificate metadata. This separation makes the code easier to test and maintain.
