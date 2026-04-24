# 📄 AI4SE — Automated IRS Document Generator

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Gemini](https://img.shields.io/badge/Google%20Gemini-8E75B2?style=for-the-badge&logo=google&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)

**Automated generation of DoD-compliant Interface Requirements Specification (IRS) documents from Capella MBSE models, powered by LLM-assisted requirement analysis.**

This pipeline extracts system interface requirements from a Capella Model-Based Systems Engineering (MBSE) model, uses Google Gemini to intelligently cluster and analyze requirements, and renders professional DoD-formatted IRS documents — including Test Plans and Test Procedures — through Jinja2 HTML templates.

---

## ✨ Key Features

- **MBSE Integration** — Directly parses Capella `.aird` / `.capella` model files to extract interface requirements
- **LLM-Powered Analysis** — Uses Google Gemini to:
  - Assign verification methods (Test, Analysis, Inspection, Demonstration)
  - Cluster requirements into logical test procedure groups
  - Generate formal technical prose for test documentation
- **DoD-Compliant Output** — Produces structured documents following defense standards:
  - Interface Requirements Specification (IRS)
  - Test Plan
  - Test Procedures
- **Automated PDF Generation** — Renders polished, print-ready PDFs via WeasyPrint
- **Fully Traceable** — Maintains requirement-to-test traceability throughout the pipeline

## 🔄 Pipeline Architecture

```
┌─────────────────┐
│  Capella MBSE   │
│  Model (.aird)  │
└────────┬────────┘
         │  Extract requirements
         ▼
┌─────────────────┐
│  Pandas DataFrame│
│  (Requirements)  │
└────────┬────────┘
         │  LLM Analysis (Gemini)
         ▼
┌─────────────────┐     ┌──────────────────────────┐
│  Clustered &    │────▶│  Jinja2 HTML Templates   │
│  Enriched Reqs  │     │  • irs_template.html     │
└─────────────────┘     │  • testplan_template.html│
                        │  • testproc_template.html│
                        └────────────┬─────────────┘
                                     │  WeasyPrint
                                     ▼
                        ┌──────────────────────────┐
                        │  PDF Documents           │
                        │  • IRS Document          │
                        │  • Test Plan             │
                        │  • Test Procedures       │
                        └──────────────────────────┘
```

## 📁 Project Structure

```
ai4se-irs-generator/
├── notebook/
│   └── IRS_Document_Pipeline.ipynb   # Main pipeline notebook (end-to-end)
├── templates/
│   ├── irs_template.html             # IRS document HTML template
│   ├── irs_testplan_template.html    # Test plan HTML template
│   └── irs_testprocedure_template.html  # Test procedure HTML template
├── data/
│   ├── SDR.capella                   # Sample Capella model
│   ├── SDR.afm                       # Model metadata
│   └── SDR.aird                      # Model interchange file
├── sample_output/                    # Example generated documents
├── requirements.txt
├── .gitignore
├── LICENSE
└── README.md
```

## 🛠️ Technologies

- **Python 3.10+** — Core language
- **Jupyter Notebook** — Interactive pipeline execution
- **Google Gemini API** — LLM for requirement analysis and content generation
- **Jinja2** — HTML template rendering engine
- **WeasyPrint** — HTML-to-PDF conversion
- **lxml** — XML parsing for Capella model files
- **Pandas** — Requirement data management
- **Capella MBSE** — Source system model (Eclipse-based)

## 🚀 Getting Started

### Prerequisites

- Python ≥ 3.10
- A Google Gemini API key

### Installation

```bash
pip install -r requirements.txt
```

### Configuration

Create a `.env` file in the project root:

```env
GOOGLE_API_KEY=your_gemini_api_key_here
```

### Running the Pipeline

1. Open `notebook/IRS_Document_Pipeline.ipynb` in Jupyter
2. Run all cells sequentially
3. Generated documents will appear in the `outputs/` directory

> **Note:** The sample Capella model (`data/SDR.*`) is included for demonstration. Replace with your own model files for production use.

## 📋 Sample Workflow

1. **Extract** — Parse Capella XML to extract interface requirements with IDs, descriptions, and source/target components
2. **Analyze** — Gemini assigns verification methods and groups requirements into test clusters
3. **Render** — Jinja2 populates DoD-formatted templates with the enriched data
4. **Export** — WeasyPrint converts the HTML to professional PDFs with proper pagination

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

## 👤 Author

**Abdullah Alghamdi** — [@aalgha7](https://github.com/aalgha7)
