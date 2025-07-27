# 📄 PDF Heading Extractor with Docker

This project automatically extracts structured headings (like H1, H2) from PDFs using a pre-trained LightGBM model. It supports multilingual documents (English, Japanese, etc.) and outputs structured JSON files for each PDF.

## 🧠 Features

- Extracts headings from PDFs using font features
- Handles multiple scripts (Latin, Japanese, etc.)
- Outputs clean JSON outlines per file
- Runs entirely inside a Docker container
- Lightweight and fast (<10s for 50-page PDFs)
- No pre-built models (built from scratch logic)

---

## 🗂 Directory Structure

```
.
├── Dockerfile
├── main.py
├── requirements.txt
├── heading_classifier_lgbm.pkl
├── input/
│   └── yourfile.pdf
└── output/
    └── yourfile.json
```

---

## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/saishivamani1/pdf-heading-extractor.git
cd pdf-heading-extractor
```

### 2. Add your model and test files
- Place your trained model file as `heading_classifier_lgbm.pkl` in the root.
- Place any test PDFs into the `input/` directory.

### 3. Build the Docker image
```bash
docker build --platform linux/amd64 -t mysolutionname:somerandomidentifier .
```

### 4. Run the container
```bash
docker run --rm \
  -v $(pwd)/input:/app/input \
  -v $(pwd)/output:/app/output \
  --network none \
  mysolutionname:somerandomidentifier
```

---

## 🧾 Output Format (`output/yourfile.json`)

```json
{
  "title": "yourfile",
  "outline": [
    {
      "level": "H1",
      "text": "Introduction",
      "page": 1
    },
    {
      "level": "H2",
      "text": "Background",
      "page": 2
    }
  ]
}
```

---

## 📦 Dependencies

All required packages are defined in `requirements.txt`. The image includes:
- Python 3.10
- PyMuPDF (`fitz`)
- LightGBM
- scikit-learn
- pandas
- joblib

---

## 🛠️ Model

The project uses a pre-trained LightGBM model trained on visual/textual features extracted from PDFs such as:
- Font size
- Font weight (bold)
- Capitalization
- Color
- Script type (Latin, Japanese, etc.)

---

## ⚠️ Notes

- Ensure your `heading_classifier_lgbm.pkl` model is trained with the same features.
- Container is isolated (`--network none`) for secure execution.
- Use PDFs that contain extractable text (non-scanned).

---

## 👨‍💻 Author

**MUNUKUNTLA SAI SHIVAMANI**  
President, Cloud Computing Club  
B.Tech AI & ML | Passionate about AI + Infrastructure

---

## 📄 License

MIT License. Feel free to use, modify, or contribute!
