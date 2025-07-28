# 📄 Round 1A: Understand Your Document

## 🚀 Overview

This solution processes a given PDF to extract a structured outline that includes the document **title** and its headings: **H1**, **H2**, and **H3** (with level and page number). It is designed to work offline, within 10 seconds for a 50-page PDF, and can be containerized for consistent and reproducible execution.

---

## 🧠 What It Does

The system:
- Automatically processes all PDFs in the `/app/input` folder.
- Uses a LightGBM-based ML model to classify PDF lines into headings (H1/H2/H3).
- Applies specific filters (e.g., restricts H3 to exactly 6 words).
- Outputs structured JSON files in `/app/output`, with one `.json` for each `.pdf`.

---

## 🗂 Input/Output Example

### ✅ Input: PDF (placed inside `/app/input/`)
Supports English, Japanese, and mixed-script PDFs.

### ✅ Output: JSON (saved inside `/app/output/`)

```json
{
  "title": "Understanding AI",
  "outline": [
    { "level": "H1", "text": "Introduction", "page": 1 },
    { "level": "H2", "text": "What is AI?", "page": 2 },
    { "level": "H3", "text": "History of AI", "page": 3 }
  ]
}
```

---

## 🛠️ How It Works

The model uses features such as:
- Font size and boldness
- Capitalization (for Latin script)
- Font name and color
- Script type (Latin or Japanese)
- Sentence length (H3 restricted to 6 words)

It extracts this data using **PyMuPDF** (`fitz`) and feeds it into a LightGBM classifier.

---

## ⚙️ Build & Run Instructions

### 🐳 Docker Build

```bash
docker build --platform linux/amd64 -t mysolutionname:somerandomidentifier .
```

### 🐳 Docker Run

```bash
docker run --rm   -v $(pwd)/input:/app/input   -v $(pwd)/output:/app/output   --network none   mysolutionname:somerandomidentifier
```

---

## 🧾 Expected Behavior

For every file `/app/input/<filename>.pdf`, it generates `/app/output/<filename>.json`.

---

## 📦 Dependencies

All dependencies are listed in `requirements.txt`:

- Python 3.10
- PyMuPDF
- pandas
- joblib
- lightgbm
- scikit-learn

---

## 📌 Constraints Compliance

| Constraint               | Status ✅        |
|-------------------------|------------------|
| ⏱ Execution time        | ≤ 10s for 50 pages |
| 📦 Model size            | ≤ 200MB           |
| 🌐 Network               | No internet used  |
| ⚙️ Runtime               | CPU-only (amd64)  |
| 📁 I/O Format            | Per PDF → Per JSON |

---

## ✅ Submission Checklist

- [x] Git project with working Dockerfile
- [x] All dependencies installed inside container
- [x] Output matches required JSON format
- [x] Docker-compatible execution (no internet, CPU-only)
- [x] README explains:
  - Approach
  - Libraries and model used
  - Build/run instructions