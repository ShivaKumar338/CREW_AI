# CrewAI — Multi-Agent Market Data Pipeline

Automated multi-agent pipeline that scrapes prediction/market sites, matches identical products across platforms, and formats results into CSV + a short market summary. Agents are orchestrated using a Crew-like `Flow` and powered by Gemini LLMs.

---

## Project structure

* `.env` — stores `GEMINI_API_KEY` (do not commit).
* `main.py` — entrypoint that defines agents, tasks, and starts the Crew flow.
* `collector.py` — `DataCollector` agent: scrapes prediction/gambling sites and collects raw product/price data.
* `matcher.py` — `ProductMatcher` agent: matches/merges identical products across different sources.
* `formatter.py` — `DataFormatter` agent: converts unified data into CSV and writes a short review/summary.
* `output/` — (generated) contains `results.csv` and `review.txt` after a successful run.

---

## Key features

* **Three-agent pipeline**: collection → matching → formatting.
* **LLM-driven agents**: agents use Gemini (e.g., `gemini/gemini-1.5-flash`) to assist with parsing, matching, and summarization logic.
* **Modular agent design**: each agent is a separate class for easy extension and testing.
* **Environment-secured API key**: `.env` is used for sensitive credentials.

---

## Prerequisites

* Python 3.8+ installed
* Virtual environment (recommended)
* Dependencies (example): `pip install -r requirements.txt` — add `crewai`, `python-dotenv`, and any scraping libraries used.

---

## Setup

1. Create and activate a virtual environment:

```bash
python -m venv venv
source venv/bin/activate   # macOS / Linux
venv\Scripts\activate    # Windows
```

2. Install dependencies (create `requirements.txt` if needed):

```bash
pip install crewai python-dotenv
# plus any scraping libs you need (requests, beautifulsoup4, selenium, etc.)
```

3. Add your Gemini API key to `.env`:

```
GEMINI_API_KEY=your_real_key_here
```

---

## Run

```bash
python main.py
```

On success you should see messages indicating the pipeline completed and files written to `output/results.csv` and `output/review.txt`.

---

## Notes & Next steps

* **Security**: Never commit `.env` or your API key to version control.
* **Extensibility**: Add more source scrapers inside `DataCollector`, improve matching heuristics in `ProductMatcher`, or extend `DataFormatter` to produce JSON/Parquet and richer reports.
* **Testing**: Add unit tests for each agent class and mocked responses for LLM calls.
* **Error handling**: Consider retries, rate-limiting handling, and logging improvements.

---

## Example agent responsibilities

* **DataCollector** — visit configured sites (Polymarket, Kalshi, etc.), extract product names, descriptions, and prices, and return a raw dataset.
* **ProductMatcher** — normalize names/descriptions, detect duplicates or the same market across platforms, and produce a unified list with canonical identifiers.
* **DataFormatter** — write the finalized unified dataset to `output/results.csv` and produce `output/review.txt` — a short market summary.

---

## License

Add a license of your choice (MIT recommended for open-source demos).

---

If you want a `README.md` adjusted for GitHub (badges, example outputs, sample CSV snippet), or a short `2-line` resume-friendly project blurb, tell me which and I will update this file.
