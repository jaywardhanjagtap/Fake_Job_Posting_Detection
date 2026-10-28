# 🕵️ Fake Job Posting Detection

An end-to-end Machine Learning and Natural Language Processing (NLP) system designed to detect fraudulent job listings using the EMSCAD (Employment Scam Aegean Dataset) containing 17,880 listings.

---

## 📌 Project Overview

Online recruitment fraud is a growing security concern targeting job seekers. This project combines:
1. **Unstructured Text Analysis**: TF-IDF vectorization on combined job posting text (company profile, description, requirements, benefits).
2. **Structured Metadata Features**: One-hot encoded categorical variables (employment type, experience, education, industry, function) along with binary flags (`telecommuting`, `has_company_logo`, `has_questions`) and text length metrics.
3. **Hybrid Feature Fusion**: Merging sparse text matrices with structured metadata matrices to train classification models with balanced class weighting.
4. **Interactive Prediction Interface**: A standalone function `predict_job_posting(...)` allowing real-time fraud probability scoring for new listings.

---

## 💾 Dataset Download (Kaggle)

Due to GitHub's file size recommendations, the raw ~50 MB CSV dataset is not hosted in this repository.

* **Download Link**: [Real / Fake Job Posting Prediction on Kaggle](https://www.kaggle.com/datasets/shivamb/real-or-fake-fake-jobposting-prediction)
* **Filename**: `fake_job_postings.csv`
* **Placement**: Download the CSV and place it directly in the project root directory before running the notebook.

```bash
# Using Kaggle CLI (optional):
kaggle datasets download -d shivamb/real-or-fake-fake-jobposting-prediction --unzip
```

---

## 📊 Model Performance Comparison

| Model | Accuracy | Precision (Fraud) | Recall (Fraud) | F1-Score (Fraud) |
| :--- | :---: | :---: | :---: | :---: |
| **Logistic Regression (Class-Balanced)** 🏆 | **96.25%** | **57.14%** | **90.17%** | **0.70** |
| **Multinomial Naive Bayes** | 95.83% | 50.34% | 84.97% | 0.63 |

> **Key Takeaway**: Because fraudulent postings represent less than 5% of the dataset, optimizing for **Recall** is critical (minimizing false negatives so job seekers are not exposed to scams). Logistic Regression achieved **90.17% Recall** on fraudulent postings while preserving >96% overall accuracy.

---

## 🔍 Key Findings & Feature Signals

- **Strong Fraud Signals**: Listings lacking company logos, lacking screening questions, or containing high-pressure phrases related to easy money, data entry, quick wire, or home-based promises.
- **Strong Genuine Signals**: Detailed company backgrounds, standard industry requirements (e.g., engineering degrees, technical proficiencies, specific benefit packages like 401(k) / healthcare).
- **Text Length**: Fraudulent listings tend to have significantly shorter descriptions and lower median word counts compared to legitimate corporate listings.

---

## 📁 Repository Structure

```text
FakeJobDetection/
├── .gitignore                      # Ignores .venv/, large CSV, checkpoints, and cache
├── README.md                       # Project documentation & Kaggle dataset link
├── requirements.txt                # Python dependencies
├── fake_job_posting.ipynb          # Main Jupyter Notebook with full analysis & pipeline
├── Fake_Job_Detection_Report.pdf   # Executive summary report (PDF) with charts
└── student_report/                 # Web report & visual assets
    ├── index.html                  # Formatted project report
    └── assets/                     # Charts (confusion matrix, missing values, ROC)
        ├── confusion.png
        ├── missing.png
        ├── modelcompare.png
        ├── preprocessing.png
        ├── structured.png
        └── textlen.png
```

---

## 🚀 Getting Started

### 1. Prerequisites
Ensure you have Python 3.10+ installed.

### 2. Clone the Repository
```bash
git clone https://github.com/<YOUR-USERNAME>/<YOUR-REPOSITORY-NAME>.git
cd FakeJobDetection
```

### 3. Download the Dataset
Download `fake_job_postings.csv` from [Kaggle](https://www.kaggle.com/datasets/shivamb/real-or-fake-fake-jobposting-prediction) and place it in the root folder.

### 4. Create and Activate a Virtual Environment
```bash
# Windows (PowerShell)
python -m venv .venv
.\.venv\Scripts\Activate.ps1

# macOS / Linux
python3 -m venv .venv
source .venv/bin/activate
```

### 5. Install Dependencies
```bash
pip install -r requirements.txt
```

### 6. Launch Jupyter Notebook
```bash
jupyter notebook fake_job_posting.ipynb
```

---

## 🧪 Live Inference Example

You can test new listings directly inside the notebook using the prediction helper:

```python
predict_job_posting(
    company_profile="We are an established tech enterprise...",
    description="We are seeking a Backend Software Engineer with experience in Python and cloud systems.",
    requirements="B.S. in Computer Science or equivalent. 3+ years experience with REST APIs and databases.",
    benefits="Comprehensive health insurance, 401(k) matching, remote flexibility.",
    has_company_logo=1,
    has_questions=1,
    employment_type="Full-time"
)
# Output: REAL ✅ (Fraud probability: ~1.17%)
```

---

## 📄 Project Reports

* **PDF Report**: Open [`Fake_Job_Detection_Report.pdf`](Fake_Job_Detection_Report.pdf) for a concise 4-page summary with visualizations.
* **HTML Report**: Open [`student_report/index.html`](student_report/index.html) in any browser for an interactive visual report.

---

## 📜 License
This project is open-source and available under the [MIT License](LICENSE).
