# Nabahan (نبهان)

**Transforming Raw Data into Intelligent Visual Stories**

An AI-Driven InsightAgent that transforms complex Etimad portal data into clear strategic insights. Using an Agentic SQL approach, it enables decision-makers to perform deep data analysis through simple natural language questions, eliminating the need for technical or programming skills.

---

## The Problem

**Who is suffering?** Strategic Decision Makers & Procurement Officers in Saudi companies who need to track thousands of daily opportunities on the Etimad platform.

**The Pain:** Information Overload - Managing thousands of new daily tenders manually is slow, exhausting, and leads to missing critical deadlines.

**Current Solution:** Manual Search & Filtering - Spending hours scrolling through the Etimad portal using basic filters.

---

## The Solution

We built an AI-Driven InsightAgent that transforms complex Etimad portal data into clear strategic insights. Using an Agentic SQL approach, it enables decision-makers to perform deep data analysis through simple natural language questions.

### Key Features

- **Multi-Agent Orchestration System** - Coordinated AI agents for scope checking, SQL generation, execution, and insight generation
- **End-to-End Data Pipeline** - Web scraping from Etimad portal, CSV processing, SQLite database, AI agents, Streamlit UI
- **Arabic-First Insight Engine** - Full RTL support with Arabic natural language understanding

---

## System Architecture

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│   Etimad     │────▶│  Web         │────▶│  CSV Files   │
│   Portal     │     │  Scraping    │     │  (Raw Data)  │
└──────────────┘     └──────────────┘     └──────────────┘
                                                 │
                                          Preprocessing
                                                 │
                                                 ▼
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│  Streamlit   │◀────│  AI Agents   │◀────│  SQLite DB   │
│     UI       │     │  (Groq LLM)  │     │  (40K+ rows) │
└──────────────┘     └──────────────┘     └──────────────┘
```

---

## The "Agentic" Logic

### The Brain (Reasoning Engine)

- **Model:** LLaMA-3.3-70B via Groq for high-speed inference
- **Why Groq?** High speed inference (~1.2s latency), allowing the Brain to process complex Arabic queries and generate SQL in real-time

### Agent Tools (The Skill-Set)

| Tool | Role | Description |
|------|------|-------------|
| `is_in_scope()` | The Gatekeeper | Scans for 20+ procurement keywords to filter out-of-scope queries |
| `generate_sql()` | The Translator | Converts Arabic to SQL with complex JOINs and schema awareness |
| `execute_sql()` | The Bridge | Safely interfaces with SQLite to fetch raw DataFrames |
| `generate_insights()` | The Analyst | Processes numbers into Arabic summaries and selects the best Plotly chart |

### Decision Process (Logic Flow)

```
User Question
     │
     ▼
┌─────────────┐     ┌─────────────────────┐
│ In Scope?   │─NO─▶│ Return: "Out of     │
└─────────────┘     │  Scope"             │
     │ YES          └─────────────────────┘
     ▼
┌─────────────┐     ┌─────────────────────┐
│ Generate SQL│─FAIL▶│ Retry (up to 3x)   │
└─────────────┘     └─────────────────────┘
     │ SUCCESS
     ▼
┌─────────────┐
│ Execute SQL │
└─────────────┘
     │
     ▼
┌─────────────┐
│ Insights    │──▶ Output: Table + Text + Chart
│ Agent       │
└─────────────┘
```

---

## Evaluation & Metrics

| Metric | Description | Target |
|--------|-------------|--------|
| **Retrieval Accuracy** | Did it find the right data? | > 80% |
| **Generation Fidelity** | Is the answer truthful to the data? | > 80% |
| **Latency** | Average query response time | < 5s |

```bash
# Run evaluation
python evaluation/run_evaluation.py

# Quick test (5 cases)
python evaluation/run_evaluation.py --quick
```

---

## Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| **Data Noise** - Scraped data from Etimad was inconsistent, with merged text in location fields | **Data Engineering** - Extensive cleaning on CSV files and standardized region names for 100% query accuracy |
| **Schema Mapping** - AI must map Arabic queries to English column names | **Self-Correction Logic** - Retry logic with fuzzy search (LIKE %) to handle naming variations and empty results |

---

## Future Work

1. **User Personalization** - Secure logins to save history and provide AI-driven business recommendations
2. **Real-time Alerts & API Integration** - Live APIs for instant data updates and automated tender notifications
3. **Data Ecosystem Expansion** - Scaling Nabahan to include diverse procurement data beyond Etimad
4. **Multi-lingual Support** - Enhancing NLP to support multiple languages for global investors

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
├── Data/                           # Raw and processed data
│   ├── raw/                        # Original scraped data from Etimad
│   └── processed/                  # Cleaned data files
│
├── Database/
│   └── nabahan.db                  # SQLite database (40K+ records)
│
├── presentation/                   # Presentation materials
├── .streamlit/                     # Streamlit configuration
├── requirements.txt                # Python dependencies
└── architecture.md                 # System architecture docs
```

---

## Tech Stack

| Component | Technology |
|-----------|------------|
| LLM | Groq API (LLaMA-3.3-70B) |
| Text-to-SQL | Vanna AI + ChromaDB |
| Database | SQLite |
| Frontend | Streamlit |
| Visualization | Plotly, Matplotlib |
| Language | Python 3.10+ |

---

## Installation

```bash
git clone https://github.com/ReAlangari/Final-Project-Nabahan.git
cd Final-Project-Nabahan

python -m venv venv
venv\Scripts\activate       # Windows
source venv/bin/activate    # Linux/Mac

pip install -r requirements.txt

# Create .env file with: GROQ_API_KEY=your_key_here

streamlit run frontend/app.py
```

---

## Conclusion

Nabahan is more than just a search tool; it is an intelligent engine utilizing Agentic AI to convert natural language into complex SQL queries with high precision. We developed this agent to break the "Big Data" barrier, transforming fragmented numbers into immediate strategic insights. With Nabahan, we don't just save time; we create insight in the era of Vision 2030.

---

## Contributor

**ReAlangari** - [github.com/ReAlangari](https://github.com/ReAlangari)

## License

This project is for educational purposes.
