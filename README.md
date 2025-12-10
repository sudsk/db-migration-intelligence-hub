# Database Migration Intelligence Hub

AI-powered semantic search system for Oracle/MSSQL to PostgreSQL migration patterns, built with BigQuery Vector Search, Vertex AI, and React.

## 🎯 Overview

The Database Migration Intelligence Hub helps database migration teams quickly find relevant patterns, troubleshooting guides, and best practices from a knowledge base of 120+ Confluence pages. Using advanced semantic search powered by BigQuery Vector Search and Vertex AI embeddings, it provides accurate results with full source citations.

## 🏗️ Architecture
```
Confluence PDFs → GCS → BigQuery/CloudSQL Vector Search → FastAPI (Cloud Run) → React App (Cloud Run)
```

**Key Technologies:**
- **BigQuery Vector Search**: Semantic search over embeddings
- **Vertex AI text-embedding-004**: Generate 768-dimensional embeddings
- **FastAPI**: Backend REST API
- **React + Next.js**: Frontend search interface
- **Terraform**: Infrastructure as Code
- **Cloud Run**: Serverless deployment

## 🚀 Quick Start

### Prerequisites

- Google Cloud Project with billing enabled
- `gcloud` CLI installed and configured
- Python 3.11+
- Node.js 18+
- Terraform 1.5+

### 1. Clone the Repository
```bash
git clone https://github.com/your-org/db-migration-intelligence-hub.git
cd db-migration-intelligence-hub
```

### 2. Set Up Environment
```bash
# Copy environment template
cp .env.example .env

# Edit with your GCP project details
vim .env
```

### 3. Run Setup Script
```bash
cd scripts/setup
./setup.sh
```

This creates:
- GCS bucket for PDFs
- BigQuery dataset and table
- Vector index for fast similarity search
- Required IAM permissions

### 4. Process PDFs
```bash
# Export Confluence pages to PDF (manual step)
# Save PDFs to local directory

# Create metadata files
cd scripts/data-processing
python create_metadata.py

# Upload PDFs and metadata to GCS
gsutil -m cp ~/confluence-exports/*.pdf gs://your-bucket/patterns/
gsutil -m cp ~/confluence-exports/*.json gs://your-bucket/patterns/

# Process PDFs to embeddings
pip install -r requirements.txt
python process_pdfs_to_bq.py
```

### 5. Run Backend
```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

Backend runs at `http://localhost:8000`

### 6. Run Frontend
```bash
cd frontend
npm install
npm run dev
```

Frontend runs at `http://localhost:3000`

## 📖 Documentation

- [Architecture](docs/ARCHITECTURE.md) - System architecture and design decisions
- [Setup Guide](docs/SETUP.md) - Detailed setup instructions
- [Usage Guide](docs/USAGE.md) - How to use the system
- [Contributing](docs/CONTRIBUTING.md) - Contribution guidelines

## 🧪 Testing
```bash
# Backend tests
cd backend
pytest

# Frontend tests
cd frontend
npm test
```

## 🚢 Deployment

### Deploy with Terraform
```bash
cd terraform/environments/prod
terraform init
terraform plan
terraform apply
```

### Manual Deploy to Cloud Run
```bash
# Backend
cd backend
gcloud run deploy intelligence-hub-api \
  --source . \
  --region us-central1 \
  --allow-unauthenticated

# Frontend
cd frontend
gcloud run deploy intelligence-hub-ui \
  --source . \
  --region us-central1 \
  --allow-unauthenticated
```

## 📊 Features

- ✅ Semantic search across 120+ migration patterns
- ✅ Full source citations (Confluence + PDF page numbers)
- ✅ PDF download with signed URLs
- ✅ Real-time similarity scoring
- ✅ Category filtering
- ✅ Responsive UI
- ✅ Infrastructure as Code with Terraform

## 🛠️ Tech Stack

**Backend:**
- FastAPI
- Google Cloud BigQuery
- Vertex AI (text-embedding-004)
- Google Cloud Storage

**Frontend:**
- Next.js 14
- React 18
- TypeScript
- Tailwind CSS

**Infrastructure:**
- Terraform
- Cloud Run
- BigQuery Vector Search
- GCS

## 📝 License

MIT License - see [LICENSE](LICENSE) file

## 🤝 Contributing

Contributions welcome! Please read [CONTRIBUTING.md](docs/CONTRIBUTING.md) first.

## 👥 Team

Built by EPAM for Deutsche Bank's Oracle to PostgreSQL migration program.

## 📧 Contact

For questions or support, please open an issue or contact the team.
