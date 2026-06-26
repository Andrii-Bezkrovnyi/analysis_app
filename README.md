# Air Raid Alerts Time Series Analyzer

An automated data pipeline and analytics tool written in Python that processes historical air raid alert logs in Ukraine, performs advanced Time Series Analysis, and utilizes Google Gemini AI to generate a comprehensive, publication-quality executive PDF report.

This project showcases an End-to-End Data Science pipeline incorporating **Data Cleaning**, **Resampling**, **Statistical Decomposition**, **Stationarity Testing**, and **Generative AI Integration** wrapped in a clean Object-Oriented Design (OOD).

---

## Key Features & Architecture

* **Object-Oriented Design (`AirRaidAnalyzer`):** Built as an extensible, modular class 
structure separating data ingestion, processing, visualization, AI reasoning, 
and document compilation.
* **Robust Data Cleaning & Outlier Filtering:** Automatically parses UTC time zones, 
calculates exact durations in minutes, and filters out system anomalies 
(e.g., negative duration records or alerts exceeding 24 hours).
* **Time Series Resampling:** Handles chronological gaps in data by reindexing the entire 
date range and backfilling days with `0` alerts, avoiding critical statistical biases 
in trend evaluation.
* **Statistical Breakdown:**
* Uses an additive **Seasonal Decomposition** model to split the raw alert signal into 
three distinct vectors: **Trend**, **Seasonality (30-day cyclic window)**, 
and **Residuals (Noise)**.
* Implements the **Augmented Dickey-Fuller (ADF) Test** to formally evaluate 
the mathematical stationarity of the series—a fundamental pre-requisite 
for auto-regressive forecasting (e.g., ARIMA).


* **Gemini 3.5 Flash Integration:** Synthesizes extracted statistics into structured 
context markers, programmatically prompting Gemini via the updated native `google-genai` 
SDK to output distinct analytical blocks natively synchronized with each visual chart.
* **Dynamic PDF Compilation (`fpdf2`):** Generates an elegant multi-page PDF document 
embedding the data visualizations alongside localized Cyrillic text layouts,
managed dynamically with page budget checking to prevent awkward chart clippings.

---

## Technology Stack

* **Core:** Python 3.10+
* **Data Engineering:** `pandas`, `numpy`
* **Statistical Modelling:** `statsmodels`
* **Data Visualization:** `matplotlib`, `seaborn`
* **Generative AI Platform:** `google-genai==2.10.0` (Gemini 3.5 Flash model)
* **Document Engineering:** `fpdf2`

---

## Project Structure

```text
├── data/
│   ├── official_data_en.csv    # Granular air raid alert logs
│   └── region_risk.csv         # Aggregated regional risk profiling data
├── main.py                     # Main execution script (AirRaidAnalyzer pipeline)
├── .env                        # Local environment file for API keys
├── requirements.txt            # Python dependencies
└── README.md                   # Project documentation

```

---

## Quick Start & Installation

### 1. Clone the Repository

```bash
git https://github.com/Andrii-Bezkrovnyi/analysis_app
cd analysis_app
```

### 2. Set Up a Virtual Environment

```bash
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

* Alternatively, install manually: 

`pip install pandas numpy matplotlib seaborn statsmodels 
fpdf2 google-genai python-dotenv`

### 4. Configure Your Environment Variables

Create a `.env` file in the root directory of the project 
and provide your Google Gemini API Key:

```env
GEMINI_API_KEY=AIzaSyYourActualGeminiApiKeyHere
```

### 5. Run the Analytics Pipeline

Ensure your data source files are stored under the `data/` directory, 
then execute the orchestrator:

```bash
python main.py
```

---

## Sample Output Pipeline

When executing, the script processes data through 7 deterministic phases:

```text
API Ключ успішно завантажено.
[1/7] Завантаження та очищення даних...
[2/7] Формирование часового ряду...
[3/7] Побудова графіків динаміки (EDA)...
[4/7] Виконання статистичної декомпозиції...
[5/7] Проведення Тесту Дікі-Фуллера...
      p-value: 0.0001 -> Стаціонарний
[6/7] Аналіз профілю ризиків за регіонами...
[7/7] Генерація ІІ-аналітики через Gemini API...
      Аналітика успішно згенерована та розбита за графіками!
>>> Формирование та збереження PDF-звіту...
Звіт успішно збережено в директорії програми: /path/to/AI_Time_Series_Report.pdf

```

### Generated Artifacts:

* **`AI_Time_Series_Report.pdf`**: The final comprehensive paper, merging daily counts, 
trend graphs, monthly cyclical patterns, regional risk mapping, 
and context-aware military-technical summaries drafted by the AI model.
* *Note:* Temporary plotting fragments (`tmp_chart_*.png`) are automatically managed 
and sanitized upon successful compilation of the core report.
---