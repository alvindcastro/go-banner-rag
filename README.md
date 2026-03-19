# Ellucian Banner Upgrade RAG Assistant (Go)

Internal Knowledge Assistant for answering questions about Ellucian Banner ERP upgrades.
Built with Go, Azure OpenAI, Azure AI Search, and Azure Blob Storage.

## Project Structure

```
banner-rag-go/
├── cmd/
│   └── main.go                  ← entry point
├── config/
│   └── config.go                ← loads .env settings
├── internal/
│   ├── azure/
│   │   ├── openai.go            ← Azure OpenAI REST client (embed + chat)
│   │   ├── search.go            ← Azure AI Search REST client (index + search)
│   │   └── blob.go              ← Azure Blob Storage SDK client
│   ├── ingest/
│   │   └── ingest.go            ← PDF parse → chunk → embed → index pipeline
│   ├── rag/
│   │   └── rag.go               ← RAG pipeline (retrieve + generate)
│   └── api/
│       ├── handlers.go          ← HTTP handlers
│       └── router.go            ← Gin route wiring
├── data/
│   └── docs/                    ← drop Banner PDFs here
├── .env.example
├── .gitignore
└── go.mod
```

## Setup

### 1. Install Go
Download from https://go.dev/dl/ — version 1.22+

### 2. Configure environment
```bash
copy .env.example .env
# Fill in your Azure credentials in .env
```

### 3. Download dependencies
```bash
go mod tidy
```

### 4. Create the Azure AI Search index
```bash
# Start the server, then call the endpoint once:
curl -X POST http://localhost:8000/index/create
```

### 5. Add Banner documents
Drop your Banner PDF release notes into `data/docs/`

Recommended naming:
```
Banner_Finance_9.3.22_ReleaseNotes.pdf
Banner_Student_9.39_ReleaseNotes.pdf
```

### 6. Run the server
```bash
go run cmd/main.go
```

### 7. Ingest your documents
```bash
curl -X POST http://localhost:8000/ingest \
  -H "Content-Type: application/json" \
  -d "{}"
```

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/health` | Check Azure connectivity |
| GET | `/index/stats` | Document count in search index |
| POST | `/index/create` | Create/recreate the search index |
| POST | `/ask` | Ask a Banner upgrade question |
| POST | `/ingest` | Ingest PDFs from data/docs/ |
| GET | `/blob/list` | List PDFs in Azure Blob Storage |
| POST | `/blob/sync` | Download from Blob + ingest |

## Example Queries

```bash
# Ask about prerequisites
curl -X POST http://localhost:8000/ask \
  -H "Content-Type: application/json" \
  -d "{\"question\": \"What are the prerequisites for Banner Finance 9.3.22?\"}"

# Filter by module and version
curl -X POST http://localhost:8000/ask \
  -H "Content-Type: application/json" \
  -d "{\"question\": \"Any known issues?\", \"version_filter\": \"9.3.22\", \"module_filter\": \"Finance\"}"

# Sync PDFs from Azure Blob then ingest
curl -X POST http://localhost:8000/blob/sync \
  -H "Content-Type: application/json" \
  -d "{\"ingest_after_sync\": true}"
```

## GoLand / GoLand Setup (Windows)

1. Open the `banner-rag-go` folder in GoLand
2. GoLand auto-detects `go.mod` — no extra config needed
3. Run `go mod tidy` in the Terminal to fetch dependencies
4. Create a Run Configuration:
   - **File:** `cmd/main.go`
   - **Working directory:** `banner-rag-go` root
5. Copy `.env.example` to `.env` and fill in Azure keys
6. Hit Run ▶
