# Nabahan (نبهان) - Saudi Government Procurement AI Agent

A Text-to-SQL AI Agent that enables natural language queries on Saudi government procurement data in Arabic, powered by **Vanna AI** and **Groq LLM**.

## Overview

Nabahan converts Arabic natural language questions into SQL queries, executes them against a structured database of Saudi government tenders and projects, and returns intelligent insights with visualizations.

### Key Features

- **Arabic Text-to-SQL** - Vanna AI + Groq LLM converts Arabic questions to SQL automatically
- **Smart Insights** - AI-generated analysis and recommendations in Arabic
- **Interactive Dashboard** - 5-page Streamlit app with full RTL Arabic support
- **Dynamic Visualizations** - Auto-generated charts (bar, pie, line) based on query results
- **Advanced Filtering** - Filter by region, entity, status, and tender type
- **Evaluation System** - Metrics and visualization for agent performance

---

## Project Structure

```
Final_Project/
├── agent/                          # Core AI Agent
│   ├── config.py                   # Configuration and prompts
│   ├── nabahan_logic.py            # Agent logic and SQL generation
│   └── vanna_setup.py              # Vanna AI + Groq integration
│
├── frontend/                       # Streamlit Web App
│   ├── app.py                      # Main application (5 pages)
│   └── components/                 # Chat, filters, visualizations
│
├── evaluation/                     # Evaluation & Metrics
│   ├── metrics.py                  # Retrieval Accuracy, Fidelity, Latency
│   ├── visualize.py                # Chart generation (Matplotlib)
│   ├── run_evaluation.py           # Evaluation pipeline runner
│   └── test_cases.json             # 20 test cases
│
├── Data/                           # Raw and processed data files
│   ├── raw/                        # Original scraped data from Etimad
│   └── processed/                  # Cleaned data files
│
├── Database/
│   └── nabahan.db                  # SQLite database (40K+ records)
│
├── presentation/                   # Presentation materials
│   ├── PRESENTATION_CONTENT.md     # 8-slide presentation content
│   └── EVALUATION_PIPELINE.md      # Evaluation pipeline docs
│
├── .streamlit/                     # Streamlit configuration
├── requirements.txt                # Python dependencies
├── architecture.md                 # System architecture docs
└── README.md
```

---

## System Architecture

```
User Query (Arabic)
       │
       ▼
┌──────────────┐
│ Scope Check  │ ──▶ Out of scope? Return message
└──────────────┘
       │
       ▼
┌──────────────┐
│  Vanna AI +  │ ──▶ Generate SQL
│  Groq LLM    │     (llama-3.3-70b-versatile)
└──────────────┘
       │
       ▼
┌──────────────┐
│   SQLite DB  │ ──▶ Execute query (7 tables, 40K+ records)
└──────────────┘
       │
       ▼
┌──────────────┐
│  Groq LLM    │ ──▶ Generate insights + chart recommendation
└──────────────┘
       │
       ▼
┌──────────────┐
│ Streamlit UI │ ──▶ Display results, insights, and charts
└──────────────┘
```

---

## Tech Stack

| Component | Technology |
|-----------|------------|
| Text-to-SQL | Vanna AI |
| LLM | Groq API (llama-3.3-70b-versatile) |
| Vector Store | ChromaDB |
| Database | SQLite |
| Frontend | Streamlit |
| Language | Python 3.10+ |
| Visualization | Plotly, Matplotlib |

---

## Database

| Table | Records | Description |
|-------|---------|-------------|
| `tenders_full_details` | 2,414 | Government tenders with full details |
| `future_projects` | 37,764 | Planned future government projects |
| `government_entity` | 1,681 | Saudi government entities |
| `regions` | 13 | Administrative regions |
| `tender_statuses` | 7 | Tender status types |
| `tender_types` | 13 | Types of tenders |
| `primary_activity` | 19 | Activity categories |

---

## Installation

```bash
# Clone
git clone https://github.com/ReAlangari/Final-Project-Nabahan.git
cd Final-Project-Nabahan

# Virtual environment
python -m venv venv
source venv/bin/activate    # Linux/Mac
venv\Scripts\activate       # Windows

# Install dependencies
pip install -r requirements.txt

# Configure API key
# Create .env file with: GROQ_API_KEY=your_key_here

# Run
streamlit run frontend/app.py
```

---

## Example Queries

| Arabic Query | Description |
|--------------|-------------|
| كم عدد المناقصات في الرياض؟ | Count of tenders in Riyadh |
| ما هي الجهات الاكثر طرحا للمنافسات؟ | Top entities by tender count |
| اعرض المشاريع المستقبلية لعام 2024 | Future projects for 2024 |
| توزيع المناقصات حسب الحالة | Tender distribution by status |

---

## Evaluation Metrics

| Metric | Description | Target |
|--------|-------------|--------|
| **Retrieval Accuracy** | Correct table and relevant data retrieved | > 80% |
| **Generation Fidelity** | Insight is truthful to the data | > 80% |
| **Latency** | Average query response time | < 5s |

```bash
# Run evaluation
python evaluation/run_evaluation.py

# Quick test (5 cases)
python evaluation/run_evaluation.py --quick
```

---

## Contributor

**ReAlangari** - [github.com/ReAlangari](https://github.com/ReAlangari)

## License

This project is for educational purposes.

---

Built with Vanna AI + Groq LLM + Streamlit
