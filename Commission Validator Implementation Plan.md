# Commission Validator using Azure AI (Mock + Real Design)

## Overview
This project outlines a system for validating PDF-based commission statements against structured commission data from CSV/API sources. It includes both a **mock implementation** (for prototyping) and a **real-world design** using Azure AI capabilities.

---

## 🔧 Use Case

- Read PDFs (cover letters, agreements, commission letters) per agent.
- Validate order of documents and data in commission letters.
- Compare against structured data (CSV/API).
- Mark as reviewed or flag for manual legal audit (10% random sample).

---

## 🧱 High-Level System Design

### Components

| Component               | Description |
|------------------------|-------------|
| Blob Storage / S3      | Store PDFs |
| Azure AI Document Intelligence / Form Recognizer | Extract text and structure from PDFs |
| Azure Functions / Python API | Orchestrate processing logic |
| Azure OpenAI / GPT-4 | Semantic validation and reasoning |
| Cosmos DB / PostgreSQL | Store review metadata |
| Logic App / Queue      | Trigger workflows / parallelize processing |
| Power BI / Email       | Reports, dashboards, alerts |

---

## ✅ Mock Implementation

### Technologies Used

- Python with `pdfplumber`, `pandas`, `random`, `os`
- Mock CSV data in-memory or as a test file
- Fake review logic: check if agent name, commission total, and ID match
- Randomly flag 10% for manual review

### Code Structure

- `main.py`: Entry point to iterate over PDFs
- `utils/parser.py`: Extract and clean text
- `utils/validator.py`: Compare PDF data vs CSV
- `mock_data/`: Sample CSVs and PDFs
- `README.md`: Docs for setup and running

### Sample Output

Each PDF gets:
- `status`: `reviewed` or `flagged_manual`
- `remarks`: Mismatches or success message

---

## 🤖 Real Implementation (Azure AI)

### Azure Capabilities

| Task | Azure Tech |
|------|------------|
| Read PDF layout | Azure Document Intelligence |
| Extract tabular commission info | Prebuilt/Custom Form Recognizer |
| Natural language validation | Azure OpenAI (GPT-4 Turbo) |
| Data source connection | Azure Data Factory / Functions |
| Orchestration | Logic Apps / Durable Functions |
| Storage | Azure Blob, Cosmos DB |
| Audit sampling | Function logic + secure tagging |

### Sample Flow

1. Upload PDF → Blob Storage
2. Trigger Function App → extract metadata via Document Intelligence
3. Retrieve API/CSV data → validate using GPT-4 prompt + code logic
4. Write result to Cosmos DB
5. Flag 10% to "manual_review" queue

---

## 📦 Real vs Mock Comparison

| Feature | Mock | Real |
|--------|------|------|
| PDF Parsing | `pdfplumber` | Azure Document Intelligence |
| Validation | Hardcoded Python | Azure OpenAI / Prompt Engineering |
| Source Input | Local CSV | API + Azure Data Factory |
| Review Logic | Random 10% | Queue + legal tag |
| Deployment | CLI/local | Azure Pipelines / App Services |

---

## 🧪 Next Steps

- Upload real PDFs and CSVs
- Replace PDF parsing with Azure Document Intelligence SDK
- Implement retry and parallel processing
- Add audit trail and role-based access
- Integrate manual review queue (e.g., Teams, Outlook, PowerApps)

---

## 🧾 Legal Compliance

- Sample 10% randomly per run
- Tag PDFs for legal QA with timestamp
- Export audit-ready logs and summary

---

## 📁 Folder Structure

```
commission_validator_prototype/
├── main.py
├── mock_data/
│   ├── sample_agent1.pdf
│   └── commissions.csv
├── utils/
│   ├── parser.py
│   └── validator.py
├── README.md
```

---

## 👨‍💻 Author & Support

Generated with help from ChatGPT. For questions or deployment guidance, raise an issue or contact your cloud solutions architect.
