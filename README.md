# Invoice OCR & Data Extraction Pipeline

This project provides an automated pipeline to extract, classify, and structure data from multi-page logistics invoices using Google Cloud AI technologies. 

## 🧠 Project Background & Approaches

This repository contains different experiments to find the most robust extraction method:

* **Direct LLM Vision (`classFactures.ipynb`)**: An initial approach using the Gemini 2.0 Flash model to directly analyze PDF pages converted to images. However, the previous single-LLM approach struggled with text detection issues.
* **Hybrid OCR + LLM Pipeline (`hybrid_ocr+llm.ipynb`)**: A refined approach implementing a hybrid solution combining Google Document AI OCR for high-precision document reading and the Vertex AI (Gemini 2.0 Flash) LLM for intelligent analysis and structured data extraction. This hybrid OCR + LLM pipeline ensures much more reliable data extraction. Thanks to the synergy between the extraction power of Document AI and the analytical intelligence of Vertex AI (Gemini), this pipeline delivers perfect detection and flawless classification of the processed documents.
* **LLM Baseline (`llm_example.ipynb`)**: A basic example demonstrating how to initialize and prompt the Vertex AI Gemini model.

## ⚙️ Prerequisites

Before running the code, ensure you have the following set up:

1. **Google Cloud Platform (GCP) Account**:
   * Enable the **Vertex AI API**.
   * Enable the **Cloud Document AI API**.
   * Create a Document AI Processor (Custom Document Extractor or General Processor) and note its ID.
2. **Authentication**: 
   * Install the Google Cloud CLI and authenticate using `gcloud auth application-default login`, OR set the `GOOGLE_APPLICATION_CREDENTIALS` environment variable pointing to your service account JSON key.
3. **System Dependencies**:
   * For `classFactures.ipynb` to work, you must install **Poppler** on your system (required by the `pdf2image` library).
     * *Windows*: Download Poppler for Windows and add the `bin` folder to your PATH.
     * *macOS*: `brew install poppler`
     * *Linux*: `sudo apt-get install poppler-utils`

## 🚀 Installation

1. Clone this repository to your local machine.
2. Create a virtual environment (recommended):
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows use: .venv\Scripts\activate

```

3. Install the required Python packages:
```bash
pip install -r requirements.txt

```



## 🛠️ Usage

### Running the Hybrid Pipeline (Recommended)

1. Open `hybrid_ocr+llm.ipynb`.
2. Update the configuration block with your GCP credentials and local paths:
```python
PROJECT_ID = "your-project-id"
LOCATION = "eu" # e.g., 'eu' or 'us'
PROCESSOR_ID = "your-processor-id"
INPUT_FOLDER = r"C:\Path\To\Your\Input\Folder"
OUTPUT_FILE = r"C:\Path\To\Your\Output\results.json"

```


3. Place your raw invoice PDFs into the designated `INPUT_FOLDER`.
4. Run all cells in the Jupyter Notebook.
5. The processed and structured JSON data will be saved to your `OUTPUT_FILE`.

### Running the Direct Vision Pipeline

1. Open `classFactures.ipynb`.
2. Update the `INPUT_FOLDER`, `OUTPUT_FILE`, and your GCP Project ID in the Vertex AI initialization block.
3. Run the notebook. The script will convert PDFs to images, analyze them, filter out duplicates/irrelevant pages, and append the results to the output JSON.

```
