
# Company Sentiment Pipeline

This project fetches recent news for a given company, analyzes sentiment, extracts entities, and stores results using **MLflow**. It leverages **LangChain**, **Gemini 2.0**, and **DuckDuckGo search**.

---

## Setup Instructions

1. **Clone the repository** (if hosted in Git):
   ```bash
   git clone <your-repo-url>
   cd <repo-directory>
   ```

2. **Create a virtual environment (recommended):**
   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux/macOS
   venv\Scripts\activate     # Windows
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Setup environment variables:**
   Create a `.env` file in the root folder (see sample below) and add your API keys.

---

## Gemini 2.0 & MLflow Configuration

1. **Gemini 2.0 Model:**
   - Requires Google API Key (`GOOGLE_API_KEY`) in `.env`.
   - Model initialized in the pipeline as `"gemini-2.0-flash"`.

2. **MLflow:**
   - Runs are tracked locally in `./mlruns` by default.
   - MLflow experiment name: `"Company Sentiment Pipeline"`.
   - MLflow callback is integrated to automatically log each pipeline run.

---

## Run the Pipeline in Jupyter Notebook

```python
# In a notebook cell
company_name = "Apple Inc"
result = run_company_sentiment(company_name)
result
```

- The result is a **structured JSON** containing:
  - `company_name`, `stock_code`, `newsdesc`, `sentiment`
  - `people_names`, `places_names`, `other_companies_referred`
  - `related_industries`, `market_implications`, `confidence_score`

---

## Notes

- If the company is not publicly listed, the stock symbol will be `"N/A"`.
- To enable MLflow logging, pass the `callbacks` argument in pipeline steps:
  ```python
  stock_code = symbol_chain.invoke({"company_name": company_name}, callbacks=callbacks)
  ```

---

## Sample `.env`

```text
# Google Gemini API Key
GOOGLE_API_KEY=your_google_api_key_here

# Optional: MLflow remote tracking URI
# MLFLOW_TRACKING_URI=http://your_mlflow_server:5000
```


