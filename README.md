# CheckWise

CheckWise is a multi-agent content forensics application that analyzes whether a text or webpage appears to be AI-written.

The application does not try to give a definitive verdict about authorship. Instead, it combines several types of signals — statistical writing patterns, grammar and polish indicators, factual claim checking, and an overall master score — to help users better understand the nature of a text.

CheckWise is designed as a structured decision aid: it highlights relevant parts of the text, explains suspicious patterns, and presents the result through multiple specialized analysis agents.

---

## About the Project

AI-generated content is increasingly common, but detecting it reliably is difficult. A simple percentage is often not enough, because users also need to understand why a text may look artificial, overly polished, repetitive, or factually uncertain.

CheckWise approaches this problem through a multi-agent system. Each agent focuses on a different aspect of the text, and the final result is obtained by combining their individual analyses.

The project supports both pasted text and webpage analysis. For webpages, the backend extracts the article content and then sends it through the same verification pipeline.

---

## Main Features

CheckWise provides:

- analysis for pasted text;
- analysis for webpage URLs;
- highlighted explanatory text spans;
- separate results from multiple agents;
- an overall AI-written likelihood score;
- factual claim extraction and verification;
- verification history saved per user;
- optional support for local and external AI models;
- fallback behavior when optional services are unavailable.

---

## How the Analysis Works

The verification process is divided into four main agents.

### Statistic Agent

The Statistic Agent analyzes measurable writing patterns such as sentence variation, linking-word repetition, linguistic style, robustness, and statistical AI-likelihood indicators.

This helps identify texts that may have overly regular rhythm, repetitive structure, or stylistic patterns commonly associated with generated content.

### Grammatical Agent

The Grammatical Agent evaluates spelling, punctuation, formatting consistency, and overall polish.

Very clean or uniform writing is not necessarily AI-generated, but it can contribute to the final analysis when combined with other signals.

### Fact-Checking Agent

The Fact-Checking Agent extracts factual claims from the text and evaluates how trustworthy they appear based on available evidence.

When external services are configured, the agent can use Gemini and Tavily for richer fact-checking. Otherwise, the application uses safe fallback results.

### Master Agent

The Master Agent combines the available agent scores into one final AI-written percentage.

This final score is meant to summarize the analysis, while the individual agent cards provide more detailed explanations.

---

## Application Flow

```text
User enters text or URL
        |
        v
Frontend sends the request to the backend
        |
        v
Backend extracts and prepares the content
        |
        v
Specialized agents analyze the text
        |
        v
Master Agent combines the results
        |
        v
Frontend displays the verdict, highlights, and history
```

## Technologies Used

### Frontend

- React
- TypeScript
- Vite
- Tailwind CSS
- Radix UI primitives
- TanStack Query
- Framer Motion
- Recharts
- Vitest

### Backend

- FastAPI
- Uvicorn
- LangGraph
- LangChain
- Ollama integration
- SQLite
- Pandas
- SciPy
- Statsmodels
- Trafilatura
- Requests

---

## Project Structure

```text
.
|-- backend/              # FastAPI backend and analysis agents
|-- checkwise_stats/      # Statistical analysis pipeline and CLI experiments
|-- src/                  # React frontend
|-- tests/                # Python tests
|-- package.json          # Frontend scripts and dependencies
|-- requirements-statistical-agent.txt
`-- vite.config.ts        # Vite configuration and API proxy
```

## Running the Project Locally

### Requirements

Before running the project, make sure you have:

- Node.js 18+ or 20+
- npm
- Python 3.10+

Optional:

- Ollama, for local model-based analysis;
- Gemini API key, for advanced claim extraction and evaluation;
- Tavily API key, for evidence search.

The project still works without these optional services, but some agents will use fallback results.

## Notes and Limitations

CheckWise produces probabilistic signals, not definitive proof of authorship.

AI detection is inherently uncertain, especially for:

- short texts;
- heavily edited texts;
- translated or paraphrased content;
- quoted material;
- bullet-heavy content;
- non-English prose;
- texts intentionally rewritten to appear more human.

The result should be interpreted as an analytical aid, not as a final judgment.

---

## Purpose of the Project

The main purpose of CheckWise is to provide a clearer and more transparent way of analyzing suspicious text.

Instead of only returning a score, the application explains the result through several perspectives: statistical structure, grammar and polish, factual reliability, and final score aggregation.

This makes the project useful not only as an AI-detection prototype, but also as an educational tool for understanding how different signals can contribute to content analysis.
