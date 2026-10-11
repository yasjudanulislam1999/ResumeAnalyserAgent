# Resume Analyser

Ranks a folder of resumes against a job description using an LLM (via [Groq](https://groq.com)).

For each resume it:
1. Extracts the text from the PDF or DOCX file
2. Uses the LLM to parse it into structured data (skills, experience, education, projects)
3. Compares it with the job description and gives a match score from 0 to 100

At the end it prints the top 2 and bottom 2 candidates with their score and details.

## Requirements

- Python 3.12+
- [uv](https://docs.astral.sh/uv/)
- A Groq API key (free at [console.groq.com](https://console.groq.com/keys))

## Setup

```bash
git clone https://github.com/yasjudanulislam1999/ResumeAnalyserAgent.git
cd ResumeAnalyserAgent
uv sync
```

Create a `.env` file in the project folder:

```
GROQ_API_KEY=your_api_key_here
```

## Usage

1. Create a `resumes/` folder and put the resumes in it (`.pdf` or `.docx`).
2. Paste the job you're hiring for into the `job_description` variable in `resume_project.py`.
3. Run:

```bash
uv run resume_project.py
```

Example output:

```
Processing: candidate_a.pdf
Score: 82.0

Processing: candidate_b.docx
Score: 64.0
...
TOP 2 CANDIDATES
Jane Doe - 82.0 %
{'matching_skills': [...], 'missing_skills': [...], 'verdict': '...'}
LOWEST 2 CANDIDATES
...
```

## Notes

- Each resume makes 2 LLM calls with a 5-second pause after each one, so you stay within Groq's rate limits. Expect about 10+ seconds per resume.
- The model is set by the `model` variable in `resume_project.py` (default `openai/gpt-oss-120b`).
- `.env` and `resumes/` are in `.gitignore`, so your API key and personal files are never committed.
