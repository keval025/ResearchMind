# ResearchMind

ResearchMind is an AI-powered research assistant. Enter a topic and its LangChain workflow searches the web, reads a relevant page, drafts a structured research report, and asks a critic agent to review it.

## Features

- Web search using Tavily
- Page scraping and text extraction
- Report generation with Google Gemini
- AI-generated critique with a score, strengths, and areas to improve
- Streamlit interface with raw research results and a Markdown report download
- Command-line pipeline for running research in a terminal

## Requirements

- Python 3.10 or later
- A Google Gemini API key
- A Tavily API key

## Setup

Open a terminal in the project directory and run:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

Create a `.env` file in the project root and add your API keys:

```dotenv
GEMINI_API_KEY=your-gemini-api-key
TAVILY_API_KEY=your-tavily-api-key
```

Keep `.env` private; do not commit real API keys to version control. For Streamlit deployments, configure `GEMINI_API_KEY` and `TAVILY_API_KEY` in the app's secrets settings instead.

## Run the Streamlit app

```powershell
streamlit run app.py
```

Streamlit opens the ResearchMind interface in your browser. Enter a topic and select **Run Research Pipeline**. The app displays search results, scraped content, the generated report, and the critic's feedback. Use **Download Report (.md)** to save the report.

## Run from the command line

```powershell
python pipeline.py
```

Enter a research topic when prompted. The pipeline prints each stage's output to the terminal.

## How it works

1. **Search agent** uses Tavily to find recent web sources.
2. **Reader agent** selects a relevant URL and extracts page text.
3. **Writer chain** uses Gemini to draft a report with an introduction, key findings, conclusion, and sources.
4. **Critic chain** reviews the report and returns a score, strengths, areas to improve, and a verdict.

The Streamlit interface is implemented in `app.py`. The command-line pipeline is in `pipeline.py`; shared agents and chains are defined in `agents.py`, and search and scraping tools are in `tools.py`.

## Configuration and notes

- The application requires both API keys to run.
- Search results and page content depend on the availability and quality of external websites and APIs.
- The reader extracts text from one selected page; verify sources and important claims before relying on a generated report.
